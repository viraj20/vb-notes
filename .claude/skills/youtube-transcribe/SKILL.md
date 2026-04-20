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

### 2.5 Present in-conversation

Report:
- Video title
- Channel / author name
- Detected subtitle language (default `en`; `youtube_transcript_api --list` shows alternates)
- Line count
- The transcript inline if ≤ 200 lines; otherwise the first 40 lines plus a note that the full text is held at `/tmp/yt-<VIDEO_ID>.txt` for the save step

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
