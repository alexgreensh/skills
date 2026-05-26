# Descript Skills

A collection of AI skills for Descript users — interactive sessions you can run with your AI assistant to get real work done, powered by [Descript](https://www.descript.com) and the [Descript API](https://docs.descriptapi.com/).

---

## What's in here

| Skill | Description | Templates |
|-------|-------------|-----------|
| [Podcast Edit](./podcast-edit/) | Turn a Zoom interview recording into a polished audio podcast | 1 workflow |
| [Blog Post Social Video](./blog-post-social-video/) | Turn any article into a 9:16 social video (30-60s) | 1 workflow |
| [ASCII Video](./ascii-video/) | Generate ASCII art video and finish in Descript | 5 templates |
| [Ramdy Creator Bootcamp](./ramdy-creator-bootcamp/) | Launch a YouTube channel from scratch, following Ramdy's Creator Bootcamp curriculum | 7 episodes |

---

## How to use these skills

### With Claude Code

Each skill folder contains a `SKILL.md` with frontmatter that Claude Code can discover and trigger automatically when placed in your commands directory.

**Install the full repo (recommended):**

```bash
git clone https://github.com/descriptinc/skills.git ~/.claude/commands/descript-skills
```

This keeps the shared `references/` folder alongside every skill so all relative paths resolve correctly.

**Install a single skill:** if you only want one skill, copy its folder and the shared `references/` folder together:

```bash
cp -r podcast-edit ~/.claude/commands/descript-skills/podcast-edit
cp -r references  ~/.claude/commands/descript-skills/references
```

### With any other AI tool

Open the `SKILL.md` file and paste its contents as a system prompt. Include the contents of `references/descript-api.md` for any Descript API-integrated skill. Then work through the session with your AI assistant.

---

## Shared references

Skills that integrate with the Descript API share a common reference file:

- **[`references/descript-api.md`](./references/descript-api.md)** — Auth setup, job polling, known limitations, and workarounds. Loaded by each Descript-integrated skill so the API knowledge stays in one place.

---

## Descript API integration

Skills in this repo that connect to Descript use the **Descript API** — currently in early access.

- **API documentation (source of truth):** [docs.descriptapi.com](https://docs.descriptapi.com/)
- **Auth:** Bearer token from Descript Settings → API tokens
- **Pattern:** Skills describe what to do and when; your MCP connection (or API client) handles the actual calls

All API-enabled steps offer a manual fallback — you can always do the same thing through the Descript app instead.

---

## Contributing

New skill series welcome. Each series should live in its own subfolder with a `SKILL.md` (including YAML frontmatter with `name` and `description`) and its own `README.md`. Shared Descript API knowledge belongs in `references/descript-api.md` rather than duplicated per skill.
