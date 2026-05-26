# Podcast Edit

An AI skill that turns a Zoom interview recording into a polished audio podcast using [Descript](https://www.descript.com) and the [Descript API](https://docs.descriptapi.com/).

---

## How to use this skill

### With Claude Code

Clone the full repo (recommended) so the shared `references/` folder is included:

```bash
git clone https://github.com/descriptinc/skills.git ~/.claude/commands/descript-skills
```

Or copy this skill folder along with the shared references:

```bash
cp -r podcast-edit ~/.claude/commands/descript-skills/podcast-edit
cp -r references  ~/.claude/commands/descript-skills/references
```

The `SKILL.md` frontmatter lets Claude Code discover and trigger the skill automatically.

### With any other AI tool

Open `SKILL.md` and paste its contents as a system prompt. Then work through the session with your AI assistant.

---

## What the workflow covers

1. **Audio cleanup** — shorten word gaps, ignore filler words (reversible, not deleted)
2. **Interview start detection** — find the real opening, skip false starts
3. **Non-destructive editing** — duplicate the composition before any cuts
4. **Section removal** — trim pre-interview, Q&A, and post-goodbye material
5. **Pull quote selection** — find 6 candidates, user picks 2-3 for the intro
6. **Timeline assembly** — intro music, pull quotes, beat bridge, interview, outro
7. **Manual fix checklist** — volume envelopes and trim points that need human ears

---

## About

Created by [Scott Kim](mailto:scott@scottkim.com) for the [Game Thinking TV](http://youtube.com/c/gamethinkingtv) YouTube channel. The workflow was built to edit Game Thinking VIP Zoom interviews into audio podcasts and is adaptable to any interview-style podcast format.
