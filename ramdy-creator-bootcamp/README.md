# Ramdy Creator Bootcamp — Skills

A series of AI skills built from [Ramdy's Creator Bootcamp](https://www.youtube.com/playlist?list=PL0SvVPop_Y6zjqTAHCISdMGBQ1jPVv87S) — a video series teaching creators everything they need to launch a YouTube channel from scratch.

Each skill takes Ramdy's advice from a single episode and turns it into an interactive session you can run with your AI assistant. Together, they walk you from zero to a fully operating channel with a content strategy, visual identity, and Descript-powered editing workflow.

---

## How to use these skills

### With Claude Code

Copy the skill files into your project's `.claude/commands/` directory (or your global `~/.claude/commands/`), then invoke them with:

```
/rcb-ep1-the-question
```

### With any other AI tool

Open the `.md` file and paste its contents as a system prompt. Then chat with your AI assistant as directed inside the skill.

---

## The series

| # | Episode | Skill | Descript integration |
|---|---------|-------|---------------------|
| 1 | The Question | `rcb-ep1-the-question` | — |
| 2 | Channel Look | `rcb-ep2-channel-look` | — |
| 3 | Generating Ideas | `rcb-ep3-generating-ideas` | — |
| 4 | Filming Your Video | `rcb-ep4-filming` | Project setup via API |
| 5 | Editing Your Video | `rcb-ep5-editing` | Script → Descript, AI editing |
| 6 | Optimizing Your Video | `rcb-ep6-optimizing` | Transcript → SEO metadata |
| 7 | Creating a Content Calendar | `rcb-ep7-content-calendar` | Batch project creation |

Episodes 4–7 connect to the Descript API to do real work inside your Descript drive — creating projects, importing scripts, generating captions, and more.

---

## How the skills chain

Each skill builds on the last. Episode 1 produces a **Creator Foundation** document. By Episode 7, you'll have a complete **Creator Profile** — a running document that captures your channel's identity, voice, content strategy, and publishing rhythm.

When each skill session ends, it will tell you exactly what to carry forward into the next one.

---

## About Ramdy

Ramdy is a creator and educator who built his Creator Bootcamp series to share the real process of making videos — not the "10 steps to go viral" stuff, but the actual mindset, decisions, and workflow that sustain a channel long-term. These skills are an extension of that work, designed to let anyone access Ramdy's framework as a repeatable, interactive coaching session.

---

## Descript API setup

For Episodes 4–7, the skills can connect to the Descript API to do real work — creating projects, importing footage, running AI edits, and retrieving published video metadata.

**API documentation (source of truth):** [docs.descriptapi.com](https://docs.descriptapi.com/)
The Descript API is early access and actively evolving. The docs are the authoritative reference — if anything in these skills conflicts with the current docs, the docs win.

**Getting a token:**
1. Go to Descript Settings → API tokens
2. Click "Create token," name it, and associate it with a Drive
3. Copy and store it securely — tokens can't be recovered after creation
4. Token permissions are scoped to the Drive it was created under

---

## How API integration works in these skills

These skills use a **directive + MCP** pattern:

- **The skill** describes *what to do* and *when* — the intent and outcome for each workflow step
- **Your MCP connection** handles *how* — the actual tool calls, request parameters, and job polling

This keeps the skills stable as the API evolves. When a skill says "create a Descript project here," it means: use your MCP tools to call the appropriate endpoint with the intent described. The MCP tool definitions reflect the current API; the skill just tells you when to use them.

**Without MCP configured:** Every skill has a manual fallback. All API steps can be done through the Descript app instead.

**Job polling:** All Descript API operations are asynchronous. Every mutating action returns a `job_id`. Poll `GET /jobs/{job_id}` until `job_state` is `"stopped"` before continuing. Use a `callback_url` if you want a webhook instead of polling.

### What each episode uses the API for

| Episode | API operation | Endpoint |
|---------|--------------|---------|
| 4 — Filming | Create project + import footage | `POST /jobs/import/project_media` |
| 5 — Editing | Agent edits: remove filler words, Studio Sound, captions, highlight reels | `POST /jobs/agent` |
| 6 — Optimizing | Retrieve published video metadata + subtitles (WebVTT) | `GET /published_projects/{slug}` |
| 7 — Calendar | Create stub projects for upcoming videos | `POST /jobs/import/project_media` |

---

*More episodes coming. Skills version-locked to bootcamp transcripts — check changelogs inside each file.*
