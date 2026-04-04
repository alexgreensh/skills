# Lyric Video

**Template:** Lyric Video
**Input:** Audio file (MP3/WAV/FLAC) + SRT file or plain text lyrics (skill will help time them if needed)

---

## Overview

ASCII art video with karaoke-style timed lyrics synced to music. An audio-reactive ASCII field serves as the backdrop while lyric text appears in the foreground with stylized effects timed to the track.

**Example use cases:** YouTube lyric video, social clip for a new single, visual accompaniment for a podcast intro quote, karaoke visual.

---

## Rendering spec

| Property | Value |
|----------|-------|
| ASCII mode | Lyrics/text — karaoke-style timed text with effects |
| Default resolution | 1920x1080 (landscape for YouTube) or 1080x1920 (portrait for social) — user picks |
| FPS | 24 |
| Duration | Matches audio |

**Background:**
- Audio-reactive ASCII field rendered at lower intensity
- Serves as backdrop, not distraction — reduce opacity/density so lyrics stay legible

**Foreground — lyric text effects:**

| Effect | Description |
|--------|-------------|
| Glow | Bloom shader applied to text characters |
| Typewriter reveal | Characters appear left-to-right within the timestamp window |
| Wave distortion | Text baseline oscillates to the beat |
| Glitch | Random character substitution at phrase boundaries or beat hits |

**Timing:**
- SRT timestamps drive text appearance and transitions
- If user provides plain text lyrics without SRT, the agent can help create timing based on audio analysis (beat detection + estimated syllable pacing)

---

## Creative brief questions

Ask all of these before writing the renderer:

1. What audio file are you working with?
2. Do you have timed SRT or plain text lyrics?
3. Visual style — minimal text on reactive background, full karaoke highlight, or text-as-particles?
4. Color scheme or brand colors?
5. Target platform (YouTube landscape, Instagram/TikTok portrait)?

---

## Example agent prompt

Use this as a starting point when writing the Python renderer. Adapt it to the user's answers from the creative brief.

> "Write a Python script that renders a lyric video. The background is an audio-reactive ASCII field — analyze [audio file] with scipy FFT, drive character density from bass energy, render at reduced opacity so it reads as backdrop. The foreground renders lyric text from [SRT file] timed to each subtitle cue. Apply a typewriter reveal effect within each cue window, a glow/bloom shader on the text, and wave distortion tied to bass amplitude. Use a cool blue palette for the background field and white for lyric text. Render at 1920x1080, 24fps, to MP4 via ffmpeg pipe."

---

## Descript finishing workflow

| Step | Action | Method |
|------|--------|--------|
| 1 | Import video + audio into project | `import_media` or manual drag-and-drop |
| 2 | Sync video and audio tracks | Manual alignment in timeline |
| 3 | Add captions for accessibility (separate from baked-in lyric visuals) | `prompt_project_agent`: "Add captions" |
| 4 | Export at target dimensions | Export at chosen platform resolution |

**Manual steps:** If the user wants intro/outro fades, volume envelopes must be drawn manually in the Descript desktop app. The API does not currently support volume ramps.
