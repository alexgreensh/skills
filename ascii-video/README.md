# ASCII Video — Skills

An AI skill that generates colored ASCII art video using a Python renderer and finishes it in [Descript](https://www.descript.com). Powered by [Descript](https://www.descript.com) and the [Descript API](https://docs.descriptapi.com/).

---

## How to use this skill

### With Claude Code

Copy the skill file into your project's `.claude/commands/` directory (or your global `~/.claude/commands/`), then invoke it:

```
/ascii-video
```

### With any other AI tool

Open the `.md` file and paste its contents as a system prompt. Then work through the session with your AI assistant.

---

## Templates

| Template | Description | Descript integration |
|----------|-------------|---------------------|
| Music Visualizer | Audio-reactive ASCII visuals synced to a track | Import + captions + Studio Sound |
| Intro Bumper | Short (5–15s) branded ASCII animation | Import + composition assembly |
| Social Clip | Portrait/square ASCII video for social platforms | Import + captions + music + export |
| Lyric Video | ASCII visuals synced to lyrics with karaoke-style text | Import + sync + captions |
| Product Launch | Product update/marketing video with ASCII aesthetic | Import + VO + Studio Sound + captions + music |

---

## What the workflow covers

1. **Environment setup** — verify Python, ffmpeg, and dependencies are installed and ready
2. **Template selection** — choose from five prebuilt templates based on your use case
3. **Creative brief** — define colors, content, duration, dimensions, and style direction
4. **Script generation** — generate the Python renderer script tailored to the chosen template
5. **Render + verify** — run the renderer locally and review the output file
6. **Import to Descript** — upload the rendered video to a Descript project via the API
7. **Descript finishing** — add captions, music, Studio Sound, voiceover, and export settings inside Descript

---

## Prerequisites

- Python 3.8+
- pip
- ffmpeg
- Python packages: `numpy`, `pillow`, `scipy`

The skill walks through setup and confirms each dependency before rendering begins.

---

## Descript API setup

This skill connects to the Descript API to import rendered video and drive post-production finishing.

**API documentation (source of truth):** [docs.descriptapi.com](https://docs.descriptapi.com/)

**Getting a token:**
1. Go to Descript Settings → API tokens
2. Click "Create token," name it, and associate it with a Drive
3. Copy and store it securely — tokens can't be recovered after creation

**Without MCP configured:** Every API step can be done manually through the Descript app instead.

---

## About

The video generation approach in this skill is built on the foundation of the [ASCII Video skill](https://github.com/NousResearch/hermes-agent/tree/main/skills/creative/ascii-video) from [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent). Their skill provides the rendering architecture and core implementation patterns for generating colored ASCII art video with Python. This skill extends that foundation with template-based creative workflows and a Descript post-production pipeline for finishing, exporting, and publishing the final video.
