# Music Visualizer

**Template:** Music Visualizer
**Input:** Audio file (MP3, WAV, or FLAC)

---

## Overview

Audio-reactive ASCII art video synced to a music track. The renderer analyzes the audio in real time and drives character density, wave distortion, color temperature, and particle effects from the frequency content and beat events.

**Example use cases:** album promo visual, social post for a new track, live stream background, DJ set visual.

---

## Rendering spec

| Property | Value |
|----------|-------|
| ASCII mode | Audio-reactive |
| Default resolution | 1080x1080 (square, social-friendly) |
| FPS | 24 |
| Duration | Matches audio length, or user-specified time range |

**Audio analysis:**
- 6-band FFT per frame (sub-bass, bass, low-mid, mid, upper-mid, high)
- Beat detection via RMS peak detection
- Spectral centroid maps to color temperature (cool blues at high centroid → warm oranges at low centroid)

**Recommended palettes by mood:**

| Mood | Palette |
|------|---------|
| Heavy / bass-driven | Block elements: `░▒▓█` |
| Ambient / chill | Braille patterns (high-density, low-contrast) |
| Electronic / cyberpunk | Katakana characters |

**Recommended effects:**
- Particle burst from center on detected beats
- Wave distortion amplitude driven by bass band energy
- Color temperature shift following spectral centroid
- Bloom shader for glow

---

## Creative brief questions

Ask all of these before writing the renderer:

1. What audio file are you working with?
2. What mood — aggressive, chill, psychedelic, minimal?
3. Any color preferences or brand colors?
4. Full track or a specific time range?
5. Target platform (YouTube, Instagram, TikTok)?

---

## Example agent prompt

Use this as a starting point when writing the Python renderer. Adapt it to the user's answers from the creative brief.

> "Write a Python script that renders an audio-reactive ASCII video. The script should analyze [audio file] using scipy FFT, extract 6 frequency bands per frame at 24fps. Map bass energy to character density using block elements (`░▒▓█`), mid frequencies to wave distortion amplitude, and spectral centroid to color temperature (cool blues → warm oranges). On detected beats, trigger a particle burst from the center. Apply bloom shader. Render at 1080x1080 to MP4 via ffmpeg pipe."

---

## Descript finishing workflow

| Step | Action | Method |
|------|--------|--------|
| 1 | Import video + audio into project | `import_media` or manual drag-and-drop |
| 2 | Sync video and audio tracks | `prompt_project_agent`: "Sync the video and audio tracks" |
| 3 | Add title/artist overlay | `prompt_project_agent`: "Add captions with the text '[song title] by [artist]'" |
| 4 | Clean up audio if needed | `prompt_project_agent`: "Add studio sound to every clip" |
| 5 | Export | Export at target platform dimensions |

**Manual steps:** If the user wants the music to fade in or out, volume envelopes must be drawn manually in the Descript desktop app. The API does not currently support volume ramps.
