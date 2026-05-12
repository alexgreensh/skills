# ASCII Video

An AI skill that generates colored ASCII art video using a Python renderer and finishes it in [Descript](https://www.descript.com). Powered by [Descript](https://www.descript.com) and the [Descript API](https://docs.descriptapi.com/).

---

## How to use this skill

### With Claude Code

Copy this skill folder into your commands directory:

```bash
cp -r ascii-video ~/.claude/commands/
```

The `SKILL.md` frontmatter lets Claude Code discover and trigger the skill automatically.

### With any other AI tool

Open `SKILL.md` and paste its contents as a system prompt. Then work through the session with your AI assistant.

---

## Templates

| Template | Description | Input |
|----------|-------------|-------|
| Music Visualizer | Audio-reactive ASCII visuals synced to a track | Audio file |
| Intro Bumper | Short (5-15s) branded ASCII animation | None or logo image |
| Social Clip | Portrait/square ASCII video for social platforms | Optional source video |
| Lyric Video | ASCII visuals synced to lyrics with karaoke-style text | Audio + lyrics/SRT |
| Product Launch | Product update/marketing video with ASCII aesthetic | Optional footage + script |

Template-specific details are in the `references/` folder. The skill loads the relevant reference when you pick a template.

---

## Prerequisites

- Python 3.8+
- pip
- ffmpeg
- Python packages: `numpy`, `pillow`, `scipy`

The skill walks through setup and confirms each dependency before rendering begins.

---

## About

Video generation approach based on the [ASCII Video skill](https://github.com/NousResearch/hermes-agent/tree/main/skills/creative/ascii-video) from [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent). This skill extends that foundation with template-based creative workflows and a Descript post-production pipeline.
