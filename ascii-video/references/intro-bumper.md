# Intro Bumper

**Template:** Intro Bumper
**Input:** None (generative), or optional logo image for ASCII conversion

---

## Overview

Short (5–15 second) branded ASCII animation for use as a channel intro, podcast video intro, or stream starting-soon screen. Pure generative or converted from a logo image.

**Example use cases:** YouTube channel intro, podcast video opener, Twitch starting-soon screen, stream overlay bumper.

---

## Rendering spec

| Property | Value |
|----------|-------|
| ASCII mode | Generative — procedural math animation |
| Default resolution | 1920x1080 (landscape) |
| FPS | 24 |
| Duration | 5–15 seconds |

**Recommended effects:**
- Coordinate transforms (rotation, scaling) for background animation
- Shader chains layered over the generative base
- Typewriter, glitch-in, or wave animation for brand name text reveal
- Brand colors mapped to color strategy (e.g., primary for text, secondary for background glow)

**If logo image provided:**
- Convert logo to ASCII using edge detection or brightness mapping
- Animate the ASCII logo in (fade, glitch, or assemble from noise)

**Design principle:** Keep tight — no filler, every frame earns its place. A 5-second bumper with strong motion is better than a 15-second one with dead air.

---

## Creative brief questions

Ask all of these before writing the renderer:

1. What is your channel or brand name?
2. Do you have a logo image, or should this be purely generative?
3. What are your brand colors?
4. What mood — techy, playful, cinematic, or glitchy?
5. Where will this be used (YouTube intro, podcast video, stream overlay)?

---

## Example agent prompt

Use this as a starting point when writing the Python renderer. Adapt it to the user's answers from the creative brief.

> "Write a Python script that renders a 10-second branded ASCII intro bumper at 1920x1080, 24fps, output to MP4 via ffmpeg pipe. Background: procedural coordinate transform animation — rotate and scale a field of ASCII block characters (`░▒▓█`) using time-based sine/cosine math. At t=2s, animate the channel name '[CHANNEL NAME]' into frame using a glitch-in effect: start each character as random symbols, resolve to the correct letter over 8–12 frames. Brand colors: map [PRIMARY COLOR] to the text and [SECONDARY COLOR] to the background glow using ANSI 24-bit color. At t=8s, hold the final logo frame for 2 seconds before cutting to black."

---

## Descript finishing workflow

| Step | Action | Method |
|------|--------|--------|
| 1 | Import rendered bumper video into project | `import_media` or manual drag-and-drop |
| 2 | Place clip as opening element in composition | `prompt_project_agent`: "Move the bumper clip to the beginning of the timeline" |
| 3 | Trim or adjust hold frame if needed | `prompt_project_agent`: "Trim the last second from the intro clip" |
| 4 | Export | Export at 1920x1080 matching episode settings |

**Manual steps:** Saving the bumper as a reusable layout or adding it to a template/layout pack must be done manually in the Descript desktop app. The API does not currently support creating or modifying layout packs.
