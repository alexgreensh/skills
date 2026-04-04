# Ramdy Creator Bootcamp — Episode 5: Editing Your Video

**Skill:** `rcb-ep5-editing`
**Series:** Ramdy Creator Bootcamp
**Episode:** 5 of 7
**Previous:** `rcb-ep4-filming`
**Next:** `rcb-ep6-optimizing`
**Descript integration:** Full — this entire episode takes place inside Descript
**Version:** 1.1

---

## What this skill does

Guides a creator through Ramdy's complete editing workflow in Descript — from importing raw files all the way to an exported, shareable video. This is the longest and most technical episode in the bootcamp.

Bring your **Creator Profile** from Episodes 1–4, and your filmed footage.

---

## Instructions for the AI

You are guiding a creator through Episode 5 of Ramdy's Creator Bootcamp. Everything from here happens inside Descript.

Ramdy's approach to editing: he's a fly-on-the-wall, uncut, showing his actual process in real time. He makes mistakes. He changes his mind. He finds out chroma key works and is pleasantly surprised. That honesty is part of what makes his editing philosophy useful — it's not "the right way," it's *his* way, and it works.

There are five stages to Ramdy's editing workflow. Walk the creator through each one in order.

---

## The five editing stages

### Stage 1 — Organize and import

Before a single edit is made, the project needs to be clean.

**File organization on disk (before opening Descript):**
Ramdy's file structure for each episode:
```
[Channel Name]/
  Episode [#] — [Title]/
    Video/
      [ProjectName]_ep[#]_raw_[description]_01.mov
      [ProjectName]_ep[#]_raw_[description]_02.mov
    Audio/
      [corresponding audio files]
    Graphics/
      Screen recordings/
        [any screen capture files]
```

The naming convention is: `ProjectName_EpisodeNumber_raw_description_takeNumber`. If they have multiple takes of the same section, they number them 01, 02, etc.

**Inside Descript:**
- Create a new project and name it
- Create matching folders: **Video**, **Audio**, **Graphics** (with a screen recordings subfolder inside Graphics)
- Import all video files into the Video folder
- Import all audio files into the Audio folder
- Import graphics and screen recordings into Graphics

Ask: "Do you have your footage organized? Walk me through what files you have."

---

### Stage 2 — Create sequences

Sequences sync your video and audio tracks into a single editable unit.

Ramdy records audio separately (via shotgun mic into an audio interface), so he needs to sync video and audio for each section. If the creator recorded audio directly to camera, this step is simpler — but still worth doing to keep things clean.

**For each section of footage (intro, main content, etc.):**
1. Select the video file and its corresponding audio file
2. Create a sequence, add speaker names
3. In the sequence view: sync the video and audio tracks using the clap at the start (or by ear if no clap was recorded)
4. Mute the camera's onboard audio track — only use the external mic audio

If they have screen recordings as part of their video, add those to the relevant sequence as an additional track.

Once all sequences are created, they're ready to edit.

---

### Stage 3 — Rough cut

**Goal:** Remove everything you don't want. No effects yet — just clean dialogue and action.

A rough cut is your entire video assembled, with:
- Retakes removed
- Dead air and micro-silences cut
- Nothing you'd be embarrassed to show someone in its current form

**Ramdy's retake workflow:**
Start by watching the **last take** of each section. The last take is usually the one he's most satisfied with. If he likes it, all previous takes get deleted. If not, he watches the take before it, and so on.

**Ramdy's pacing obsession:**
He is "very anal about dead spaces between cuts." Even 0.1-second silences between cuts bother him. He wants the edit to feel like a continuous, constant flow — unless a pause is playing comedically, in which case he keeps it.

**AI tool shortcut — Shorten Word Gaps:**
In Descript, go to AI tools > **Shorten Word Gaps**. This automatically compresses the spaces between words across the whole sequence. Ramdy does this before manually fine-tuning — it saves significant time on unscripted sections where thinking pauses are everywhere. You can always re-add a gap if you want one back.

**Editing instinct, not just mechanics:**
Ramdy also makes judgment calls about *what to cut*, not just silence. He asks:
- Is this section too boring? (Cut it.)
- Does this play comedically? (Keep it.)
- Am I just reading at the camera instead of reacting? (Cut more of the passive reading, keep the moments where he's commenting or engaging.)

Work through their rough cut section by section. Ask: "How's the flow feeling? Is there anything that drags?"

---

### Stage 4 — Picture lock

**Goal:** Finalize everything the viewer *sees*. All effects, zoom-ins, graphics, text, B-roll, and visual elements are added here. Once you're done with a section in picture lock, you don't touch it again.

Ramdy's process: he watches the video section by section and adds visual elements wherever they'd improve the shot. He doesn't plan most of this in advance — it's reactive, intuitive.

**Key techniques and Descript features used:**

**Zoom-ins and punch-ins**
Ramdy creates these by splitting a clip into two scenes — one with the original framing, one zoomed in — then adding a **Smart Transition** between them. Descript animates the transition automatically. He uses these constantly because they make longer sections feel shorter and more engaging.

**Slow zooms**
For gradual zooms across multiple clips: select all the clips in that section, add a keyframe animation, set the start and end frames, and change easing to "None" for a linear zoom.

**Layout packs**
Descript's layout packs let you create a saved visual style (background color, text font, graphic positions) that you can apply consistently across the video. Ramdy builds one custom layout pack for each project and applies it throughout. Saves time, keeps the look consistent.

Layouts to know:
- **Camera layout** — just the full camera shot
- **Screen recording layout** — puts the screen share as the main content with the camera smaller in the corner (multiple size options)
- Custom layouts they create

**B-roll**
Add relevant video clips to support or react to what's being said. Descript has a built-in media library. Ramdy layers B-roll with color adjustments (e.g., blue tone for a "sad" moment) to match the emotional beat of the section.

**Text and graphics**
Use the text tool to add titles, lower thirds, or callout text. Ramdy animates text with slide-in effects. He pairs these with font choices that match his channel's visual identity.

**Chroma key (green screen)**
If they have green screen footage, apply the Chroma Key effect to remove the background. Then layer other clips or graphics behind the now-transparent background layer. Duplicate the script layer, mute the duplicate's audio, and apply chroma key to the duplicate — this way the original audio plays while the visual gets keyed out.

**Adding objects behind the presenter**
Duplicate the camera layer → mute the audio on the duplicate → apply Chroma Key to the duplicate → place graphics or video *between* the original layer and the duplicate. The result: objects appear behind the presenter in the scene.

Ask: "Walk me through what your video needs visually — lots of talking-head content? Screen recordings? B-roll? Graphics?" Then help them plan which techniques apply.

---

### Stage 5 — Final mix

**Goal:** Add all music and sound effects. This is the last thing before export.

Ramdy's philosophy on audio in the final mix:

> "Sound effects and music take it to that other level of feeling engaging and immersed. It's not even that much work — it's finding the right music, the right effects, and the right levels."

**Music:**
Search Descript's built-in music library. Find something that matches the energy of the section. Layer it underneath the dialogue track.

**Audio level tip:** In Descript settings, enable "Show volume in dB" instead of percentage. This is standard across editing programs and makes it easier to work with. Set levels in **clip audio** (not the main audio panel) — this way the volume gets copied when you duplicate a clip.

General starting points:
- Background music: –14 to –16 dB
- Sound effects (punchy): –6 to –10 dB
- Sound effects (subtle/ambient): –12 to –18 dB

Always adjust to taste and listen back after setting.

**Sound effects:**
Descript has a sound effects library. Add a sound to any cut, transition, or visual moment where audio would enhance the joke or punctuate the edit. Common approaches:
- Whoosh/swoosh for fast visual movements or transitions
- Ambient sounds layered under B-roll (pan audio left/right to match screen position)
- Reaction sounds (error buzzes, dings, etc.) for comedic beats

**Studio Sound:**
At any point in the process (Ramdy uses it during rough cut on his shotgun mic footage), apply **Studio Sound** via AI tools. It cleans up background noise and improves clarity, especially if the mic wasn't perfectly positioned. Run it, then listen back and judge.

---

### Descript API — Agent editing shortcuts

> The Descript API is early access and actively evolving. These skills describe **intent** — what to do and when. Your MCP connection handles **how** — exact parameters, error handling, and polling. If anything has changed, [docs.descriptapi.com](https://docs.descriptapi.com/) is the source of truth.

**Operation:** `POST /jobs/agent`

The Descript agent (Underlord) can automate specific mechanical editing tasks via natural language prompt. These are **supplements to the manual workflow** — they handle repeatable tasks so the creator focuses on the creative decisions that require judgment.

**Critical constraint:** Agent prompts are one-shot only. There is no multi-turn back-and-forth. Frame each instruction as a complete, self-contained request with all the context the agent needs upfront.

**After each agent call:** Poll `GET /jobs/{job_id}` until `job_state` is `"stopped"` before proceeding. The `project_url` in the response lets the creator open the updated project.

#### What the agent can do at each stage

**Stage 3 — Rough cut:**

| Task | Prompt to use |
|------|--------------|
| Remove filler words ("uh," "um," etc.) | `"Remove all filler words from the transcript"` |
| Apply Studio Sound to all clips | `"Add studio sound to every clip"` |

**Stage 4 — Picture lock:**

| Task | Prompt to use |
|------|--------------|
| Add rendered captions to the video | `"Add captions"` |

**Stage 5 — Final mix:**

| Task | Prompt to use |
|------|--------------|
| Cut a 30-second highlight reel | `"Create a 30-second highlight reel"` |
| Remove a specific section by timestamp | `"Remove the section from [timestamp] to [timestamp]"` |
| Custom edit described in plain language | Write a complete one-shot description of the edit |

#### What the agent cannot do

The agent handles mechanical edits. It cannot make aesthetic judgments — it won't decide which take is funnier, what B-roll fits the emotional beat, or where a zoom-in would land. Ramdy's five-stage workflow still requires a human for the creative layer. The agent is the assistant, not the editor.

**Targeting a specific composition:** The `composition_id` parameter on the agent endpoint is currently marked as work in progress. Target by `project_id` and describe the section you want edited in the prompt itself.

**If Descript MCP is not configured:** All editing is done manually inside Descript using the five stages above. Underlord is also accessible directly in the Descript UI for any of these same tasks.

---

### Export

When the final mix is done:

**Export video:**
- Go to the Export tab
- Select your max resolution (4K if you shot in 4K, 1080p otherwise)
- Recommended: Use **Descript web link** instead of local export
  - Publishes the video to a shareable link
  - Anyone can watch from the link (collaborators, clients, friends for feedback)
  - Download the final video from the share page when ready

**Export SRT (subtitles):**
Descript's transcript is accurate and already timed. Export it as an SRT file. You'll upload this in Episode 6 when you post the video to YouTube — it gives you accurate, embedded captions instead of YouTube's auto-generated ones.

**Export timeline (optional):**
If you want to do additional work in Premiere Pro, After Effects, Final Cut, or DaVinci, export the Descript timeline in your preferred format. You don't have to give up your other tools to use Descript — it integrates.

---

### Building the Editing entry

Add this to their Creator Profile:

```
## Video Edit
[Added: Episode 5]

Descript project name: [name]
Rough cut: [complete / in progress]
Picture lock: [complete / in progress]
Final mix: [complete / in progress]

Descript share link: [URL for review/download]
SRT file exported: [yes / pending]

Descript features used:
  [ ] Studio Sound
  [ ] Shorten Word Gaps
  [ ] Layout pack
  [ ] Smart transitions
  [ ] Chroma key
  [ ] A/B test thumbnails (next episode)
```

---

### Homework

> "Edit your video. Use Ramdy's five stages as your guide. Remember to take breaks — editing is a marathon — and try things, make mistakes, and have fun with it.
>
> If you get stuck on a specific Descript feature, use **Underlord** (the AI assistant in Descript) and tell it what you're trying to do. It will walk you through it."

---

### Handoff to Episode 6

> "Your video is edited and exported. There's a Descript link sitting there that you can share with anyone who wants to watch it before it goes live.
>
> Episode 6 is about uploading and optimizing — thumbnails, titles, descriptions, upload settings, subtitles. All the stuff that determines whether anyone clicks on your video.
>
> Bring your SRT file, your Creator Profile, and run:
>
> `/rcb-ep6-optimizing`
>
> Almost there. See you then, soldier."

---

## What this skill does NOT do

- It does not edit your video for you. Ramdy's workflow requires judgment calls — what to cut, what to keep, what looks funny. That's your job.
- It does not cover advanced color grading. Ramdy does minimal color work and keeps it simple.
- It covers Descript's core editing tools, not every feature. Use Underlord inside Descript for anything not covered here.

---

## Source

Based on the transcript of [Ramdy Creator Bootcamp Episode 5 — "Editing Your Video"](https://www.youtube.com/playlist?list=PL0SvVPop_Y6zjqTAHCISdMGBQ1jPVv87S).
All core advice, philosophy, and framing belongs to Ramdy.
Descript feature references reflect the product as used in the bootcamp; see [Descript's documentation](https://help.descript.com) for the latest.
