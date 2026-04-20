---
name: youtube-transcribe
description: Extract a transcript from a YouTube URL and present it in-conversation. Triggers "youtube transcript", "extract subtitles", "get the transcript", "transcribe this video". Uses youtube-transcript-api as the primary extractor (bypasses YouTube's PO Token gate), with yt-dlp and Chrome DevTools MCP as fallbacks. Writes NOTHING to disk unless the user explicitly says save/capture.
---

# YouTube Transcript Extraction

Extract subtitles from a YouTube video and show them in-conversation. Do NOT write a file or compile wiki pages unless the user explicitly asks to save.

Input YouTube URL: $ARGUMENTS

## Step 1: Verify URL

Confirm the input is a valid YouTube URL (`youtube.com/watch?v=`, `youtu.be/`, `youtube.com/shorts/`). Extract the 11-character video ID. If no URL is provided, check the recent conversation for a link.

## Step 2: Extract via youtube-transcript-api (primary)

This library calls YouTube's caption endpoint directly and sidesteps the PO Token / n-challenge gates that now block yt-dlp on most videos. Prefer it first.

### 2.1 Check tool availability

Run `which youtube_transcript_api`. If not installed:

```bash
pipx install youtube-transcript-api
```

(pipx lives at `/usr/local/bin/pipx` on this Mac; `brew install yt-dlp` path is blocked by `/usr/local` permissions — use pipx.)

### 2.2 Fetch the transcript as JSON

```bash
youtube_transcript_api <VIDEO_ID> --format json > /tmp/yt-<VIDEO_ID>.json
```

If it errors with "no transcripts available" or "transcripts disabled", fall through to Step 3 (yt-dlp) or Step 4 (Chrome DevTools MCP).

### 2.3 Fetch the video title via YouTube oEmbed

```bash
curl -s "https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=<VIDEO_ID>&format=json"
```

Parse `title` and `author_name` from the JSON. No auth, no cookies needed.

### 2.4 Convert JSON to timestamped plain text

The transcript JSON is a list of `{text, start, duration}` segments. Convert to `[HH:MM:SS] text` or `[MM:SS] text` (omit hours if < 1h). One segment per line. Save to `/tmp/yt-<VIDEO_ID>.txt`.

Example Python inline:

```bash
python3 -c "
import json
segs = json.load(open('/tmp/yt-<VIDEO_ID>.json'))[0]
out = []
for s in segs:
    t = int(s['start']); m, sec = divmod(t, 60); h, m = divmod(m, 60)
    ts = f'{h:02d}:{m:02d}:{sec:02d}' if h else f'{m:02d}:{sec:02d}'
    out.append(f'[{ts}] ' + s['text'].replace(chr(10),' ').strip())
open('/tmp/yt-<VIDEO_ID>.txt','w').write('\n'.join(out))
print(f'LINES={len(out)}')
"
```

### 2.5 Generate a structured point summary (ALWAYS)

After extraction succeeds, produce a bullet-point summary of the video. This runs every time, not just on save — it lives in the conversation and gets saved with the source if the user asks.

**Goal**: preserve the author's **meaning, tone, and intent**. Do not sanitize strong opinions. Do not add caveats the author didn't voice. Do not paraphrase into generic business-speak — keep the author's voice intact.

**Structure:**

```markdown
## <Title> — <Channel>

**Stance.** 1–2 sentences: where the author is coming from, who they're pushing back against, what they're selling or arguing for.

**Main points:**

1. **<Short point headline>.**
   - Claim: <the claim, with the author's exact numbers>
   - Argument: <how they justify it, in their framing>
   - Example / evidence: <their specific example; quote punchy phrases verbatim in "quotes">

2. **<Next point>.**
   - …

**Asides / bonus.**
- <tangents, bonus picks, side tips the author slipped in>

**Close.** What the author wants the viewer to do next (subscribe, join community, buy something, act on a timeline).
```

**Rules for the summary:**

- Use the author's numbers exactly (percentages, dollar amounts, dates) — no rounding unless they rounded.
- Quote punchy or distinctive phrases verbatim in `"quotes"`. Keep code-switched Hindi/English if present; it's part of the voice.
- Preserve tone: if the author is dismissive, sound dismissive; if confident, sound confident; if self-promoting, say so.
- Follow the video's own ordering unless a different order is materially clearer.
- Don't add warnings, balanced perspectives, or caveats the author didn't state. Not your job to fact-check.
- Length: scale to the video — ~300 words for <10 min, ~600 words for 20–30 min, ~900+ for long-form.

### 2.6 Present in-conversation

Report, in this order:

1. **Metadata table** — title, channel, language, line count, duration (approx from last timestamp).
2. **Transcript preview** — full inline if ≤ 200 lines; otherwise the first 40 lines, with a note that the full text is held at `/tmp/yt-<VIDEO_ID>.txt`.
3. **The structured summary** from Step 2.5.

**Do NOT save to `sources/`. Do NOT run `/ingest-url`. Do NOT create wiki pages.**

## Step 3: yt-dlp fallback

Only use if `youtube-transcript-api` failed (e.g., "no transcripts available", or the video uses custom captions that the API can't fetch).

**Known caveat**: yt-dlp currently hits YouTube's PO Token / n-challenge gate on most videos and fails with "Requested format is not available." Expect this to fail more often than it succeeds.

### 3.1 Check and invoke

```bash
~/.local/bin/yt-dlp --cookies-from-browser=chrome \
  --write-auto-sub --write-sub --sub-lang en,en-US,en-GB \
  --skip-download --extractor-args "youtube:player_client=web" \
  --output "/tmp/yt-%(id)s.%(ext)s" "<URL>"
```

(Use `~/.local/bin/yt-dlp` to bypass the broken `/usr/local/bin/yt-dlp` shebang.)

If it lands a `.vtt` file, read it, strip VTT headers/styling tags/duplicate lines, and continue to Step 2.5.

## Step 4: Chrome DevTools MCP fallback

Only if Steps 2 and 3 both fail AND Chrome DevTools MCP tools are present in the session:

1. `new_page` on the video URL.
2. `take_snapshot` to read the accessibility tree.
3. Find and `click` the description's "...more" / "Show more" button to expand it.
4. `take_snapshot` again. Find and `click` "Show transcript" / "显示转录稿".
5. `evaluate_script` with:

   ```javascript
   () => {
     const segments = document.querySelectorAll("ytd-transcript-segment-renderer");
     if (!segments.length) return "BUFFERING";
     return Array.from(segments)
       .map(seg => {
         const time = seg.querySelector(".segment-timestamp")?.innerText.trim();
         const text = seg.querySelector(".segment-text")?.innerText.trim();
         return `${time} ${text}`;
       })
       .join("\n");
   };
   ```

Retry up to 3 times if the result is `"BUFFERING"`. Then `close_page` and continue to Step 2.5.

If all three extraction paths fail, stop and tell the user which tools are missing or broken.

## Step 5: Save ONLY on explicit request

Only write the transcript when the user says "save it," "capture this," "write it to sources," or similar.

When asked to save:

1. **Route the domain** per `CLAUDE.md`. Default: `learning`. Override if the user says otherwise, or if the channel is clearly finance (e.g., Akshat Shrivastava, Zerodha, Groww) or entertainment.
2. **Sync first**: `git pull --rebase origin main`.
3. **Write** to `sources/<domain>/youtube/<YYYY-MM-DD>-<slug>.md` where `<slug>` is kebab-case of the title (lowercase, hyphenated, strip specials, cap at 60 chars).
4. **Frontmatter** per `CLAUDE.md` source schema:

   ```yaml
   ---
   url: <original YouTube URL>
   author: <channel name from oEmbed>
   captured: <YYYY-MM-DD>
   captured_via: youtube-transcript
   wiki_compiled: false
   ---
   ```

5. **Body**: the full timestamped transcript below the frontmatter.
6. **Log** under `## [YYYY-MM-DD HH:MM] youtube-transcribe-save <URL>` in `wiki/log.md`.
7. **Commit + push** per CLAUDE.md sync protocol:
   ```bash
   git add -A
   git diff --cached --quiet || git commit -m "youtube-transcribe: <video title>"
   git push origin main
   ```
8. **Do NOT auto-invoke `/ingest-url`.** The source is queued (`wiki_compiled: false`) for the next manual ingest run.

## Not this skill's job

- Compiling wiki pages from the transcript — that's `/ingest-url`.
- Classifying into `wiki/synthesis/` — synthesis is a promotion target, never a capture destination (per CLAUDE.md).
- Summarizing the video's content unless the user asks.
