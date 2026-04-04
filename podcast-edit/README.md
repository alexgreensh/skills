# Podcast Edit — Skills

An AI skill that turns a Zoom interview recording into a polished audio podcast using [Descript](https://www.descript.com) and the [Descript API](https://docs.descriptapi.com/).

---

## How to use this skill

### With Claude Code

Copy the skill file into your project's `.claude/commands/` directory (or your global `~/.claude/commands/`), then invoke it:

```
/podcast-edit
```

### With any other AI tool

Open the `.md` file and paste its contents as a system prompt. Then work through the session with your AI assistant.

---

## The skill

| Skill | Description | Descript integration |
|-------|-------------|---------------------|
| `podcast-edit` | Full workflow: cleanup, trimming, pull quote selection, timeline assembly | Full — transcript editing, filler removal, composition assembly via API |

---

## What the workflow covers

1. **Audio cleanup** — shorten word gaps, ignore filler words (reversible, not deleted)
2. **Interview start detection** — find the real opening, skip false starts
3. **Non-destructive editing** — duplicate the composition before any cuts
4. **Section removal** — trim pre-interview, Q&A, and post-goodbye material
5. **Pull quote selection** — find 6 candidates, user picks 2–3 for the intro
6. **Timeline assembly** — intro music, pull quotes, beat bridge, interview, outro
7. **Manual fix checklist** — volume envelopes and trim points that need human ears

---

## Descript API setup

This skill connects to the Descript API for transcript-based editing and composition assembly.

**API documentation (source of truth):** [docs.descriptapi.com](https://docs.descriptapi.com/)
The Descript API is early access and actively evolving. The docs are the authoritative reference — if anything in this skill conflicts with the current docs, the docs win.

**Getting a token:**
1. Go to Descript Settings → API tokens
2. Click "Create token," name it, and associate it with a Drive
3. Copy and store it securely — tokens can't be recovered after creation

**Without MCP configured:** Every API step can be done manually through the Descript app instead.

---

## About

Created by [Scott Kim](mailto:scott@scottkim.com) for the [Game Thinking TV](http://youtube.com/c/gamethinkingtv) YouTube channel. The workflow was built to edit Game Thinking VIP Zoom interviews into audio podcasts and is adaptable to any interview-style podcast format.
