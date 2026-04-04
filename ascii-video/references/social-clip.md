# Social Clip

**Template:** Social Clip
**Input:** Optional source video to convert, or none (generative)

---

## Overview

Portrait or square ASCII art video optimized for social platforms — TikTok, Instagram Reels, YouTube Shorts, X posts. Can convert existing footage to ASCII or generate from scratch.

**Example use cases:** repurpose a product demo as a stylized TikTok, create a generative brand loop for Instagram Reels, make a short ASCII teaser for a YouTube Shorts drop.

---

## Rendering spec

| Property | Value |
|----------|-------|
| ASCII mode | Video-to-ASCII (if source provided) or generative |
| Default resolution | 1080x1920 (portrait) or 1080x1080 (square) — user picks platform |
| FPS | 24 |
| Duration | 15–60 seconds |

**If source video:**
- Edge detection for sharp ASCII character mapping
- Motion tracking to preserve subject clarity across frames
- Character set selected to match edge density of input footage

**If generative:**
- Particle systems with procedural animation
- No source footage required — fully algorithmic

**Character grid:**
- Higher density grids for small-screen readability (more characters per row/col than standard)
- Recommended: use a dense character set like braille or fine ASCII to preserve detail at mobile viewing sizes

---

## Creative brief questions

Ask all of these before writing the renderer:

1. Source footage to convert, or fully generative?
2. Target platform — TikTok, Instagram Reels, YouTube Shorts, or X?
3. What is the video about / what message should it convey?
4. Color vibe — neon, monochrome, pastel, or specific brand colors?
5. Any text overlays needed (title, call to action, handle)?

---

## Example agent prompt

Use this as a starting point when writing the Python renderer. Adapt it to the user's answers from the creative brief.

> "Write a Python script that renders a 30-second portrait ASCII social clip at 1080x1920 and 24fps. If a source video is provided, apply edge detection and motion tracking to map frames to high-density ASCII characters — use a fine character set for small-screen readability. If generative, build a particle system with procedural animation. Apply a neon color palette (hot pink, cyan, electric green on a dark background). Export to MP4 via ffmpeg pipe."

---

## Descript finishing workflow

| Step | Action | Method |
|------|--------|--------|
| 1 | Import rendered video (and audio if source had audio) | `import_media` or manual drag-and-drop |
| 2 | Add captions | `prompt_project_agent`: "Add captions — large text, centered, optimized for mobile" |
| 3 | Add background music | Add a track from Descript's built-in music library |
| 4 | Export at platform dimensions | Export at 1080x1920 (portrait) or 1080x1080 (square) |

**Manual steps:** Background music selection and level adjustment must be done in the Descript desktop app. The API does not currently support browsing or auditioning the built-in music library.
