# ASCII Video — Generate ASCII Art Video and Finish in Descript

**Skill:** `ascii-video`
**Descript integration:** Full — media import and agent-based editing via Descript API
**Version:** 1.0

---

## What this skill does

A coding agent writes a bespoke Python renderer that outputs colored ASCII art as real MP4 video. You pick a template (music visualizer, intro bumper, social clip, lyric video, product launch), answer a few creative questions, and the agent generates the video from scratch. Then you import it into Descript for finishing — captions, music, voiceover, export.

---

## Instructions for the AI

You are guiding a creator through generating an ASCII art video and finishing it in Descript. The workflow has two phases: **video generation** (Steps 1-5) and **Descript post-production** (Steps 6-7).

The video generation step involves writing a single-file Python renderer from scratch — this is the core approach. The renderer uses NumPy + Pillow + ffmpeg to render colored ASCII characters as actual video frames. No pre-built templates or binaries — the agent writes the script each time based on the creative brief.

After rendering, the video is imported into Descript for post-production: captions, music, voiceover, and export.

> The Descript API is early access and actively evolving. This skill describes **intent** — what to do and when. Your MCP connection handles **how**. If anything has changed, [docs.descriptapi.com](https://docs.descriptapi.com/) is the source of truth.

**After every `prompt_project_agent` or `import_media` call:** Poll `get_job` until `job_state` is `"stopped"` and check `result.status` for `"success"` or `"error"` before proceeding.

---

## The workflow

Work through these steps in order.

### Step 1: Environment setup

Start by asking: "Before we begin, do you already have Python 3, ffmpeg, and the required Python packages (numpy, pillow, scipy) installed? If yes, we can skip setup. If not, I'll walk you through it."

If setup is needed, guide per OS:

- **macOS:** `brew install ffmpeg` then `pip install numpy pillow scipy`
- **Linux:** `sudo apt install ffmpeg` then `pip install numpy pillow scipy`
- **Windows:** Download ffmpeg from [ffmpeg.org](https://ffmpeg.org), add to PATH, then `pip install numpy pillow scipy`

Verify everything works:

```bash
python3 -c "import numpy, PIL, scipy; print('Ready')"
ffmpeg -version
```

Both commands should succeed before moving on.

### Step 2: Pick a template

Present the five templates:

| Template | Description | Input |
|----------|-------------|-------|
| Music Visualizer | Audio-reactive ASCII visuals synced to a track | Audio file |
| Intro Bumper | Short (5-15s) branded ASCII animation | None or logo image |
| Social Clip | Portrait/square ASCII video for TikTok/IG/Shorts | Optional source video |
| Lyric Video | ASCII visuals synced to lyrics with karaoke-style text | Audio + lyrics/SRT |
| Product Launch | Product update/marketing video with ASCII aesthetic | Optional footage + script |

Once the user picks a template, read the corresponding reference file from `references/` for template-specific details.

### Step 3: Creative brief

Ask the template-specific questions from the reference file, plus these universal questions:

- **Target resolution:** Landscape (1920x1080), portrait (1080x1920), square (1080x1080), or custom?
- **Target duration?**
- **Color preferences or brand colors?**

### Step 4: Generate the Python script

Write a single-file Python renderer based on the creative brief and the template's rendering spec. Save it as a `.py` file the user can run directly.

#### Rendering guidance

This section gives the agent enough to write a working renderer without external dependencies beyond numpy, pillow, scipy, and ffmpeg.

**Architecture:** Single Python file. Core loop: for each frame, build a pixel canvas (uint8 numpy array H x W x 3), composite colored ASCII characters onto it using pre-rasterized font bitmaps, pipe raw RGB frames to ffmpeg via subprocess.

**Font rasterization:** Use Pillow to render each ASCII character once at the target font size, cache as numpy arrays. Common monospace fonts: "Menlo" (macOS), "Consolas" (Windows), "DejaVu Sans Mono" (Linux). Fall back through the list until one loads.

**Character palettes:** Density ramps (light to dark): ` .:-=+*#%@`. Block elements: `░▒▓█`. Braille patterns for high-density fields. Pick palette based on mood and template.

**Color:** Map source data (audio FFT bands, video luminance, procedural math) to RGB values. For perceptual color, use OKLAB/OKLCH color space conversions.

**Audio analysis (for audio-reactive modes):** Use scipy FFT to extract 6 frequency bands per frame. Detect beats via peak detection on RMS energy. Map spectral centroid to color temperature.

**Video sampling (for video-to-ASCII modes):** Use ffmpeg subprocess to decode input video frames. Sample luminance to select characters. Optionally apply edge detection for sharper ASCII mapping.

**Tonemap:** ASCII on black backgrounds is inherently dark. Use adaptive percentile-based tonemapping (`np.percentile` on the canvas, then rescale) to ensure the output isn't muddy.

**Shaders:** Composable post-processing effects applied per-frame: bloom (gaussian blur + additive blend), chromatic aberration, scanlines, vignette, color grading. Chain multiple shaders.

**ffmpeg output:** Pipe raw RGB frames to ffmpeg via `subprocess.Popen`:

```bash
ffmpeg -f rawvideo -pix_fmt rgb24 -s WxH -r FPS -i pipe: -c:v libx264 -pix_fmt yuv420p output.mp4
```

For GIF output: add `-vf "fps=15,scale=640:-1"`.

**Common pitfalls:**

1. **macOS font height** can be wrong — measure actual rendered height, not reported height.
2. **ffmpeg pipe deadlock** — if you don't read stderr, the pipe can deadlock. Use `communicate()` or a separate thread for stderr.
3. **NumPy broadcasting errors** are the #1 crash — always verify array shapes before operations.

For deeper reference material on effects, shaders, and advanced techniques, see the [NousResearch ASCII Video skill](https://github.com/NousResearch/hermes-agent/tree/main/skills/creative/ascii-video).

### Step 5: Render and verify

Run the script. Confirm:

- **Output file exists**
- **Duration matches expectation:** `ffprobe -v error -show_entries format=duration -of csv=p=0 output.mp4`
- **Resolution matches spec:** `ffprobe -v error -select_streams v:0 -show_entries stream=width,height -of csv=p=0 output.mp4`
- **File size is reasonable** — not 0 bytes, not absurdly large

If the render fails, debug common issues: ffmpeg not found, font not available, numpy broadcasting errors, ffmpeg pipe deadlock.

Ask the user to watch the rendered video and confirm they're happy with it before proceeding. For video-to-ASCII conversions, render a short preview (5s) first so the user can approve the look before committing to the full render.

### Step 6: Import to Descript

Ask: **"Do you want to manually upload your media to Descript, or import via the API?"**

**If manual:**

Tell the user to drag and drop the rendered video (and any source audio files) into their Descript project via the desktop app. Ask for the project link once done (looks like `https://web.descript.com/<project-id>`).

**If API:**

Guide the user to upload the rendered MP4 to their cloud storage service of choice (Dropbox, Google Drive, S3, etc.) and get a publicly accessible URL. Then:

1. Call `import_media` with the public URL to create a new project or add to an existing one
2. If the template involves source audio (music visualizer, lyric video, product launch), that file also needs a public URL — import it alongside the video
3. Poll `get_job` until complete

> **Note:** The Descript API does not currently support local file upload — media must be at a publicly accessible URL. This limitation is expected to change. See [docs.descriptapi.com](https://docs.descriptapi.com/) for the latest capabilities.

### Step 7: Descript finishing

Run the opinionated finishing workflow defined in the template's reference file. Use `prompt_project_agent` for each operation.

After each agent call, poll `get_job` until `job_state` is `"stopped"` and check `result.status` for `"success"` or `"error"`.

Note any steps that require manual attention in the Descript desktop app (the reference file will specify these).

---

## Key principles

- **One file, one render.** The Python script is self-contained — no external dependencies beyond numpy, pillow, scipy, and ffmpeg.
- **Fresh script every time.** The agent writes the renderer from scratch based on the creative brief, not from a template.
- **Show before you cut.** For video-to-ASCII conversions, render a short preview (5s) first so the user can approve the look before committing to the full render.
- **Claude can't see video.** All quality judgments about the rendered video require the user to watch it. The agent verifies technical specs (duration, resolution, file size) but not visual quality.
- **Jobs are async.** After every Descript API call, poll with `get_job` until the job state is stopped. Check `result.status` for success or error.

---

## Known API limitations

| Limitation | Workaround |
|-----------|-----------|
| **No local file upload via API** | Upload to cloud storage, use public URL; or drag-and-drop into Descript desktop app |
| **No volume ramps / gain envelopes** | Draw manually in Descript desktop app |
| **Agent is one-shot** | Frame each instruction as a complete, self-contained request |
| **composition_id is WIP** | Target by `project_id`, describe composition by name in prompt |

These limitations reflect the API as of early 2026. Check [docs.descriptapi.com](https://docs.descriptapi.com/) for the latest capabilities — as the API evolves, some of these workarounds may no longer be necessary.

---

## What this skill does NOT do

- Does not ship a pre-built video renderer. The agent writes the Python script each time.
- Does not play or preview rendered video. The user must watch it to judge visual quality.
- Does not automate volume envelopes or crossfades in Descript.
- Does not handle video hosting — the user manages cloud storage for API import.
- Does not support local file upload via the Descript API (yet).

---

## Source

> Video generation approach based on the [ASCII Video skill](https://github.com/NousResearch/hermes-agent/tree/main/skills/creative/ascii-video) from [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent). The rendering architecture, effect catalogs, shader system, and single-file Python approach originate from that skill.
>
> Descript API references reflect the product as of early 2026; see [docs.descriptapi.com](https://docs.descriptapi.com/) for the latest.
