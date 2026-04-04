# Descript Skills

A collection of AI skills for Descript users — interactive sessions you can run with your AI assistant to get real work done, powered by [Descript](https://www.descript.com) and the [Descript API](https://docs.descriptapi.com/).

---

## What's in here

| Series | Description | Episodes |
|--------|-------------|----------|
| [Ramdy Creator Bootcamp](./ramdy-creator-bootcamp/) | Launch a YouTube channel from scratch, following Ramdy's Creator Bootcamp curriculum | 7 (more coming) |
| [Podcast Edit](./podcast-edit/) | Turn a Zoom interview recording into a polished audio podcast | 1 |

---

## How to use these skills

### With Claude Code

Copy a skill file into your project's `.claude/commands/` directory (or your global `~/.claude/commands/`), then invoke it:

```
/rcb-ep1-the-question
```

### With any other AI tool

Open the `.md` file and paste its contents as a system prompt. Then work through the session with your AI assistant.

---

## Descript API integration

Skills in this repo that connect to Descript use the **Descript API** — currently in early access.

- **API documentation (source of truth):** [docs.descriptapi.com](https://docs.descriptapi.com/)
- **Auth:** Bearer token from Descript Settings → API tokens
- **Pattern:** Skills describe what to do and when; your MCP connection (or API client) handles the actual calls

All API-enabled steps offer a manual fallback — you can always do the same thing through the Descript app instead.

---

## Contributing

New skill series welcome. Each series should live in its own subfolder with its own `README.md` following the conventions in this repo.
