# Blog Post → Social Video — Skills

An AI skill that turns any blog post or article into a polished 9:16 social video (30–60s) inside [Descript](https://www.descript.com). Powered by [Descript](https://www.descript.com) and the [Descript API](https://docs.descriptapi.com/).

---

## How to use this skill

### With Claude Code

Copy the skill file into your project's `.claude/commands/` directory (or your global `~/.claude/commands/`), then invoke it:

```
/blog-post-social-video
```

### With any other AI tool

Open the `.md` file and paste its contents as a system prompt. Then paste your article text and let the AI guide you through the workflow.

---

## What the workflow covers

1. **Script** — condenses the article into a punchy 30–60s voiceover (hook → key points → takeaway)
2. **Brand setup** — uses provided brand assets or researches the brand automatically via web search
3. **Style reference** — establishes a visual DNA from provided images or generates hero candidates with Nano Banana Pro
4. **Project + format** — creates a new Descript project in 9:16 vertical format
5. **Voiceover** — generates VO with a confident AI voice
6. **Scene map** — plans all 8–12 scenes with timing before touching the timeline
7. **Layout remix** — applies brand colors and fonts to a caption-forward layout
8. **Visual generation** — generates two still candidates per scene via Nano Banana Pro, selects the best, then animates each with Veo 3.1 image-to-video
9. **Edit assembly** — builds the timeline with clean hard cuts and minimal cross-dissolves
10. **Captions** — applies branded, legible captions in the safe zone
11. **Logo overlay** — places a consistent corner bug (if logo provided)
12. **Outro** — generates a branded end card with CTA
13. **Music + mix** — adds an instrumental bed with proper VO ducking and compression
14. **Final QC** — verifies every constraint before delivery

---

## Global constraints

| Constraint | Rule |
|------------|------|
| **TEXT_FREE** | All AI-generated imagery must contain zero text. Hard-fail — discard and regenerate if violated. |
| **SCENE_CAP** | No scene may exceed 8.0 seconds. |
| **STYLE_LOCK** | All b-roll generated via Nano Banana Pro (edit) with the PRIMARY STYLE REFERENCE attached — no Descript style picker. |
| **AUTO_EXECUTE** | No approval checkpoints. Proceeds automatically through all steps. |

---

## Input

| Asset | Required |
|-------|----------|
| Article text (title + body) | Required |
| Hero / supporting images | Optional |
| Brand logo | Optional |
| Brand colors | Optional |
| Brand fonts | Optional |

---

## Descript API setup

This skill connects to the Descript API to create projects and drive post-production finishing.

**API documentation (source of truth):** [docs.descriptapi.com](https://docs.descriptapi.com/)

**Getting a token:**
1. Go to Descript Settings → API tokens
2. Click "Create token," name it, and associate it with a Drive
3. Copy and store it securely — tokens can't be recovered after creation
