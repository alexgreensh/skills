# Blog Post Social Video

An AI skill that turns any blog post or article into a polished 9:16 social video (30-60s) inside [Descript](https://www.descript.com). Powered by [Descript](https://www.descript.com) and the [Descript API](https://docs.descriptapi.com/).

---

## How to use this skill

### With Claude Code

Copy this skill folder into your commands directory:

```bash
cp -r blog-post-social-video ~/.claude/commands/
```

The `SKILL.md` frontmatter lets Claude Code discover and trigger the skill automatically.

### With any other AI tool

Open `SKILL.md` and paste its contents as a system prompt. Then paste your article text and let the AI guide you through the workflow.

---

## What the workflow covers

1. **Script** — condenses the article into a punchy 30-60s voiceover
2. **Brand setup** — uses provided brand assets or researches the brand automatically
3. **Style reference** — establishes visual DNA from provided images or generates hero candidates
4. **Project + format** — creates a new Descript project in 9:16 vertical format
5. **Voiceover** — generates VO with a confident AI voice
6. **Scene map** — plans all 8-12 scenes with timing before touching the timeline
7. **Visual generation** — generates stills via Nano Banana Pro, animates with Veo 3.1
8. **Edit assembly** — builds the timeline with crossfade transitions
9. **Captions** — applies branded, legible captions in the safe zone
10. **Logo overlay** — places a consistent corner bug (if logo provided)
11. **Outro** — generates a branded end card with CTA
12. **Music + mix** — adds an instrumental bed with proper VO ducking
13. **Final QC** — verifies every constraint before delivery
