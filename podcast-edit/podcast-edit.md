# Podcast Edit — Turn a Zoom Recording into a Polished Audio Podcast

**Skill:** `podcast-edit`
**Descript integration:** Full — transcript-based editing, filler word removal, composition assembly via Descript API
**Version:** 1.0

---

## What this skill does

Walks you through turning a raw Zoom interview recording into a polished audio podcast using Descript and the Descript API. You bring the recording; this skill handles the editorial workflow — from cleanup through final assembly.

The result is a complete podcast episode with intro music, pull quotes, a beat bridge, the edited interview, and an outro.

---

## Instructions for the AI

You are guiding a podcast producer through a structured editing workflow. All editorial decisions are made from the **transcript** — you cannot hear audio. That means every cut point needs human confirmation with surrounding context shown.

The workflow is sequential and non-destructive by default. Filler words are ignored (muted), never deleted. Destructive cuts happen only in a duplicated composition, never the original. Always show 10–15 words of transcript context around a proposed cut point and get approval before proceeding.

> The Descript API is early access and actively evolving. This skill describes **intent** — what to do and when. Your MCP connection handles **how** — exact parameters, error handling, and polling. If anything has changed, [docs.descriptapi.com](https://docs.descriptapi.com/) is the source of truth.

**After every `prompt_project_agent` call:** Poll `GET /jobs/{job_id}` (via `get_job`) until `job_state` is `"stopped"` and check `result.status` for `"success"` or `"error"` before proceeding.

---

## Final podcast structure

```
intro music + announcer
  → pull quotes (over quieter music)
    → beat music bridge
      → interview
        → ending music fade-in
          → guest goodbye
            → outro music + announcer URL
```

---

## The workflow

Work through these steps in order. **Always check in with the user before making any destructive cut.**

### Step 1: Get the Descript project

The user uploads the recording manually via the Descript desktop app. Direct file upload from Claude's sandbox is blocked by network restrictions, and Google Drive links require authentication Descript can't satisfy.

Ask for the project link once upload is done. It looks like `https://web.descript.com/<project-id>`.

### Step 2: Clean up audio mechanics

Run these two operations back-to-back without checking in — they're safe and reversible.

**2a. Shorten word gaps** to a maximum of 0.3 seconds throughout the composition.

**2b. Ignore filler words** — mark them as ignored (muted from playback), not deleted. Ignoring is reversible; deletion is not.

Filler words to catch: um, uh, like (filler use only), you know, right (rhetorical), so (sentence-opener), basically, literally, actually, essentially, yeah (standalone), absolutely (filler response).

**Descript API — Steps 2a and 2b:**

| Task | Agent prompt |
|------|-------------|
| Shorten word gaps | `"Shorten all word gaps to a maximum of 0.3 seconds"` |
| Ignore filler words | `"Remove all filler words from the transcript"` |

### Step 3: Find the real interview start

Search the transcript for a keyword the host typically uses to open the interview — often "welcome" in the first 5 minutes. Show the user **10 words before and after** each occurrence found.

Watch for false starts: "welcome" immediately followed by an interruption, crosstalk, or "hold on / wait" is a false start. Look for the next clean occurrence that flows naturally into the guest introduction.

Ask the user to confirm which occurrence is the real start. Note the exact timestamp.

### Step 4: Duplicate the composition

Before any destructive cuts, duplicate the composition and name the copy using the format:

```
[episode-id] [guest-first-name] [guest-last-name] AUDIO PODCAST
```

Example: `yt395 chelsea howe AUDIO PODCAST`

All subsequent edits happen in the new copy. The original stays untouched as a backup.

**Descript API:**

| Task | Agent prompt |
|------|-------------|
| Duplicate and rename | `"Duplicate the current composition and rename the copy to '[name]'"` |

### Step 5: Trim the pre-interview intro

Delete everything before the confirmed start word from Step 3.

**Descript API:**

| Task | Agent prompt |
|------|-------------|
| Trim intro | `"Remove everything from the beginning of the composition up to [timestamp]"` |

### Step 6: Find and remove the Q&A section

Many interview podcasts include a live Q&A that should be cut. Search the transcript for:

- **Q&A start:** The host inviting audience questions ("does anyone have a question", "let's open it up", etc.)
- **Goodbye start:** The host's closing thank-you to the guest ("thank you so much", "this was so inspiring", etc.)

Show the user **15 words of context** around each cut point and get approval. Then delete everything between Q&A start and goodbye start.

**Descript API:**

| Task | Agent prompt |
|------|-------------|
| Remove Q&A section | `"Remove the section from [Q&A start timestamp] to [goodbye start timestamp]"` |

### Step 7: Trim the ending

Check what follows the goodbye. Describe any post-goodbye material (crosstalk, anecdotes, dead air).

Target ending: **2–4 sentences total** — the host's thank-you + the guest's first brief acknowledgment (e.g., "Of course. Absolutely."). Do not carry through anecdotes, extended compliments, or sign-offs to the audience.

Confirm the cut point with the user, then make the cut.

### Step 8: Select pull quotes

Search the full transcript for **6 candidate pull quotes** from the guest. A good pull quote is:

- **Short** — ideally 10–20 words, one or two sentences
- **Provocative or counterintuitive** — makes the listener curious without fully satisfying it
- **Self-contained** — understandable without context
- **A bold claim, surprising insight, or vivid specific detail**

For each candidate, show: the exact quote text, timestamp, and one sentence explaining why it works.

Present all 6 and offer your top picks. The user selects 2–3, totaling about 30 seconds of audio. Order them: snappy/conceptual first to hook the listener, funny/specific last.

### Step 9: Add standard media files to the project

Standard audio files (intro music, beat/bridge music, outro) typically live in Descript's shared media library or a team drive. The Descript API **cannot** pull from the shared library automatically — the user must manually drag them into the project's media panel in the desktop app.

Ask the user to confirm:
1. What their standard media files are called
2. That they've been added to the project's media panel

Once confirmed, proceed to Step 10.

### Step 10: Assemble the timeline

Send a single detailed prompt to `prompt_project_agent` describing the full structure. Be explicit about placement and ordering:

1. **Intro music** as background track from time 0. Announcer section plays first.
2. **Pull quotes** start after the announcer section ends, in the order the user selected. Music continues underneath.
3. **Beat bridge music** on a separate background track — placed to start before the last pull quote ends, rising to full volume after the last pull quote, holding briefly, then fading as the interview begins.
4. **Interview** plays in full.
5. **Ending music** as background track starting ~10 seconds before the final goodbye word.
6. **Outro music + announcer** placed immediately after the interview ends.

Ask the agent to report what it was and wasn't able to do.

> **Volume envelopes:** The Descript API cannot automate volume ramps or gain envelopes. The agent will place clips at the right positions, but volume shaping must be done manually in the desktop app (see Step 11).

### Step 11: Manual fixes (always required)

After assembly, tell the user these always need manual attention in the desktop app:

- **Intro music fade-out** — add a manual volume fade where the intro music ends so it doesn't cut abruptly
- **Beat bridge volume shape** — the bridge music clip is placed at the right position, but draw the volume envelope manually: low for ~4s, swell to full as pull quotes end, hold ~2s, fade down through the first ~4s of the interview
- **Ending music fade-in** — the ending music starts at full volume; draw a fade-in over the ~10 seconds before the goodbye
- **Pull quote trim points** — clips may have small amounts of surrounding audio at the edges; listen and tighten as needed

---

## Key principles

- **Tight is better.** Short intros, tight endings, no dead air.
- **Always show context before cutting.** Paste 10–15 words around any proposed cut point and get approval before destructive changes.
- **Ignore filler words, never delete them.** Ignoring is reversible; deletion is not.
- **Duplicate before destructive edits.** Always work in a named copy, not the original.
- **Watch for false starts.** The first keyword hit is often a false start — verify before cutting.
- **Claude can't hear audio.** All cut decisions are transcript-based. Pull quote trim points and music fades always need a human ear.
- **Jobs are async.** After calling `prompt_project_agent`, poll with `get_job` until the job state is stopped. Check `result.status` for success or error.

---

## Customization

This skill was built around the Game Thinking VIP interview format, but the workflow applies to any interview-style podcast. To adapt it:

- **Step 3:** Change the keyword used to find the interview start (e.g., "welcome", "let's get started", "today we're talking to")
- **Step 6:** Skip if your format doesn't include a Q&A section
- **Steps 9–10:** Swap in your own standard media files and adjust the timeline structure to match your podcast format
- **Pull quote criteria (Step 8):** Adjust based on your audience — what counts as "provocative" depends on context

---

## Known API limitations

| Limitation | Workaround |
|-----------|-----------|
| **Shared media library** — the API cannot import files from the drive-level shared media library | User manually drags files into the project's media panel |
| **Volume ramps / gain envelopes** — no API support for fade curves | Draw manually in Descript's desktop app |
| **Audio playback** — Claude cannot listen to audio | All decisions are transcript-based; manual review required for audio quality |
| **Google Drive imports** — requires auth Descript can't satisfy | Use Dropbox with `dl=1` links, or upload directly |
| **composition_id** — targeting a specific composition is work-in-progress | Target by `project_id` and describe the composition by name in the prompt |
| **Agent is one-shot** — no multi-turn conversation | Frame each instruction as a complete, self-contained request |

These limitations reflect the API as of early 2026. Check [docs.descriptapi.com](https://docs.descriptapi.com/) for the latest capabilities — as the API evolves, some of these workarounds may no longer be necessary.

---

## What this skill does NOT do

- It does not play or listen to audio. All editorial decisions are transcript-based.
- It does not automate volume envelopes or crossfades. Those require manual work in Descript.
- It does not import media from shared libraries or Google Drive. The user handles file management.
- It does not make creative judgment calls about what sounds good. It proposes; you decide.

---

## Source

Based on the podcast editing workflow created by [Scott Kim](mailto:scott@scottkim.com) for the [Game Thinking TV](http://youtube.com/c/gamethinkingtv) YouTube channel. Scott built the original skill to edit Game Thinking VIP Zoom interviews into audio podcasts using Descript and the Descript API.

Descript API references reflect the product as of early 2026; see [docs.descriptapi.com](https://docs.descriptapi.com/) for the latest.
