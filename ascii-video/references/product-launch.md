# Product Launch

**Template:** Product Launch
**Input:** Optional screen recording or product footage + script/talking points. Can also be fully generative with TTS narration.

---

## Overview

Product update or marketing video with an ASCII art aesthetic. Eye-catching alternative to the standard screen recording + voiceover format.

**Example use cases:** feature announcement, product update social post, launch trailer, email embed, landing page hero video.

---

## Rendering spec

| Property | Value |
|----------|-------|
| ASCII mode | Hybrid (video-to-ASCII with generative overlays) if source footage; generative with TTS if no footage |
| Default resolution | 1920x1080 (landscape) |
| FPS | 24 |
| Duration | 30–90 seconds |

**Mode selection:**
- If source footage provided: hybrid mode — video-to-ASCII conversion with generative overlays for transitions and emphasis moments
- If no footage: generative mode with text sections showing feature names, stats, and URLs
- If TTS: ElevenLabs integration (requires API key) — generates speech from script, rendered with typewriter text effect synced to audio

**Section structure:**

| Section | Duration |
|---------|----------|
| Hook | 3–5s |
| Problem / context | 10–15s |
| Feature showcase (main body) | Remaining |
| CTA | 5–10s |

---

## Creative brief questions

Ask all of these before writing the renderer:

1. What product or feature are you announcing?
2. Do you have screen recordings or product footage?
3. Do you have a script or talking points?
4. Will there be voiceover — recorded separately or TTS?
5. What are your brand colors?
6. What tone — hype, understated, technical, or playful?
7. Where will this be published?

---

## Example agent prompt

Use this as a starting point when writing the Python renderer. Adapt it to the user's answers from the creative brief.

> "Write a Python script that renders a 60-second product launch video in hybrid mode. Convert the provided screen recording to ASCII using character density mapping, then layer generative transition overlays at section boundaries. Structure the video as: 5-second hook with bold centered text → 15-second problem context section → feature showcase body → 5-second CTA with URL. Brand colors: [primary] and [secondary]. Apply generative ASCII overlays at each section transition for visual emphasis. Render at 1920x1080 at 24fps to MP4 via ffmpeg pipe."

---

## Descript finishing workflow

| Step | Action | Method |
|------|--------|--------|
| 1 | Import video (+ audio if separate VO or TTS output) | `import_media` or manual drag-and-drop |
| 2 | If voiceover not baked in: add VO track | Record in Descript or import VO file manually |
| 3 | Apply Studio Sound | `prompt_project_agent`: "Add studio sound to every clip" |
| 4 | Add captions | `prompt_project_agent`: "Add captions" |
| 5 | Add background music | Use Descript's built-in music library; suggest low-energy or ambient tracks |
| 6 | Export | Export at target dimensions |

**Manual steps:** Background music level adjustment and any VO/music fade transitions need manual work in the Descript desktop app. The API does not currently support volume ramps.
