---
name: youtube-transcribe
description: Extract a transcript from a YouTube URL and present it in-conversation. Triggers "youtube transcript", "extract subtitles", "get the transcript", "transcribe this video". Uses yt-dlp (CLI) with Chrome DevTools MCP as fallback. Writes NOTHING to disk unless the user explicitly says save/capture.
---

# YouTube Transcript Extraction

Extract subtitles from a YouTube video and show them in-conversation. Do NOT write a file or compile wiki pages unless the user explicitly asks to save.

Input YouTube URL: $ARGUMENTS

## Step 1: Verify URL

Confirm the input is a valid YouTube URL (`youtube.com/watch?v=`, `youtu.be/`, `youtube.com/shorts/`). If none is provided, check the recent conversation for a link.

## Step 2: Extract via yt-dlp (primary)

### 2.1 Check tool availability

Run `which yt-dlp`. If not installed, tell the user: `brew install yt-dlp`, or fall back to Step 3 if Chrome DevTools MCP is available.

### 2.2 Get video title

```bash
yt-dlp --cookies-from-browser=chrome --get-title "<URL>"
```

If a browser-cookie error occurs, ask the user for their browser (`firefox`, `safari`, `edge`, `brave`) and retry. Default `chrome`.

### 2.3 Download subtitles to a temp path

```bash
yt-dlp --cookies-from-browser=chrome --write-auto-sub --write-sub \
  --sub-lang en,zh-Hans,zh-Hant --skip-download \
  --output "/tmp/yt-%(id)s.%(ext)s" "<URL>"
```

### 2.4 Convert to plain text

Read the `.vtt` or `.srt` file from `/tmp/`. Strip headers, styling tags, and duplicate lines. Produce entries of the form `Timestamp Text`, one per line.

### 2.5 Present in-conversation

Report:
- Video title
- Detected subtitle language
- Line count
- The transcript inline if ≤ 200 lines; otherwise the first 40 lines plus a note that the full text is held for the save step

**Do NOT save to `sources/`. Do NOT run `/ingest-url`. Do NOT create wiki pages.**

## Step 3: Chrome DevTools MCP fallback

If `yt-dlp` is unavailable but Chrome DevTools MCP tools are present:

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

Retry up to 3 times if the result is `"BUFFERING"`. Then `close_page` and continue to Step 2.5 (present only, do not save).

If neither `yt-dlp` nor Chrome DevTools MCP is available, stop and tell the user which to install.

## Step 4: Save ONLY on explicit request

Only write the transcript when the user says "save it," "capture this," "write it to sources," or similar.

When asked to save:

1. **Route the domain** per `CLAUDE.md`. Default: `learning`. Override if the user says otherwise or the channel is clearly finance/entertainment.
2. **Sync first**: `git pull --rebase origin main`.
3. **Write** to `sources/<domain>/youtube/<YYYY-MM-DD>-<slug>.md` where `<slug>` is kebab-case of the title (lowercase, hyphenated, strip specials, cap at 60 chars).
4. **Frontmatter** per `CLAUDE.md` source schema:

   ```yaml
   ---
   url: <original YouTube URL>
   author: <channel name>
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
