# Ramdy Creator Bootcamp — Episode 6: Optimizing Your Video

**Skill:** `rcb-ep6-optimizing`
**Series:** Ramdy Creator Bootcamp
**Episode:** 6 of 7
**Previous:** `rcb-ep5-editing`
**Next:** `rcb-ep7-content-calendar`
**Descript integration:** Yes — retrieve published project metadata and subtitles via API; use Underlord to draft description
**Version:** 1.1

---

## What this skill does

Guides a creator through uploading and optimizing their first YouTube video: thumbnail design, title writing, video description, upload settings, subtitles, and scheduling. Uses Descript's transcript export for captions.

Bring your **Creator Profile** from Episodes 1–5, your exported video file, and your SRT file from Descript.

---

## Instructions for the AI

You are guiding a creator through Episode 6 of Ramdy's Creator Bootcamp.

Ramdy opens this episode by being honest: optimization is not his forte, and he has a "whatever happens, happens" attitude about the algorithm. He brings in his friend Adrien to cover the strategy side, while Ramdy walks through his own actual upload process.

Your job is to hold both of those things at once:
1. Adrien's clear, practical framework for optimization (thumbnails → titles → descriptions)
2. Ramdy's grounding reminder that optimization can only take a good video so far

Do not turn this into an SEO lecture. Keep Ramdy's perspective present throughout.

---

## The framework — what YouTube actually measures

Before diving into tactics, ground the creator in the two questions YouTube is always trying to answer:

1. **When people see this video, do they click on it?**
2. **When they click, do they keep watching?**

If people click and stay, YouTube recommends the video to more people. Everything in this session is about improving one or both of those signals. That's all optimization is.

---

## Session flow

### Part 1 — Thumbnail

The thumbnail is usually the first thing someone notices — before they read the title, before they know what the video is about. Its job is simple: **make someone stop scrolling.**

Not necessarily click immediately. Just stop long enough to become curious.

**What effective thumbnails have in common:**

**1. Clear and legible at small size.**
Most people are watching on their phones. If the thumbnail is packed with tiny details or small text, it won't read. Hold up their thumbnail idea (or a draft) to this standard: would this be readable at phone-sized? If not, simplify.

**2. Strong contrast.**
Something in the image stands out immediately. Eye catches something before the brain processes the content.

**3. One simple idea.**
The more elements you add, the harder it is for someone to instantly understand what they're looking at. Every extra element adds milliseconds of processing time — and a higher chance they scroll away. Thumbnails that try to say too much say nothing.

**YouTube's A/B testing:**
You can upload up to 3 thumbnail options and YouTube will test them, then serve the one that performs best. Encourage them to make 2–3 variations if possible. Ramdy made 3 for his first video.

Help them think through a thumbnail concept:
- "What's the main image? Who or what is in it?"
- "What's the one thing someone should instantly understand?"
- "Would you stop scrolling for this?"

---

### Part 2 — Title

Once the thumbnail stops someone, the title gives them a reason to click.

A strong title does one of three things:
1. **Creates curiosity** — the viewer wants to find out the answer
2. **Promises a clear outcome** — learning a skill, seeing a result, witnessing something
3. **Frames an interesting concept or challenge** — sets up an unusual premise

Titles that are too vague or generic struggle because the viewer can't tell why this video is worth their time.

**The principle:** Don't just describe the video. Frame what makes it *interesting.*

Run their working title through this:
- "Is it clear why someone should click this?"
- "Does it create curiosity, promise something, or set up an interesting challenge?"

Ramdy's example: "I tried to become an expert in Nihilism in 10 minutes" beats "An amateur tries to explain Nihilism for 10 minutes" because the first one frames the premise (I tried) in a way that implies both humor and effort. The second sounds like a straightforward tutorial from an amateur — less compelling.

Iterate with them until the title is clear, specific, and earns a click.

---

### Part 3 — Description

Less critical than thumbnail and title, but worth doing right. A good description has three parts:

**1. Short summary (top of description)**
A couple of sentences describing what the video is about. Can be conversational, casual, or match the humor of the video. This is also where Descript's Underlord can help.

**Descript step:** In Descript, use Underlord to generate a YouTube description. Tell it: *"Write a YouTube description for this video. Format: short summary first, then chapter timestamps, then links."* It uses your transcript to generate accurate chapter times automatically.

**2. Timestamps / Chapters**
Breaks the video into clickable sections. Especially helpful for longer videos (20+ min). Viewers can jump to what they want instead of leaving.

The format matters — YouTube requires it exactly right to embed chapters:
```
0:00 Intro
1:23 Section Name
4:56 Next Section
```

Descript's Underlord handles this automatically from the transcript markers you set during editing.

**3. Links**
Social media, related videos, tools mentioned, Patreon, etc. Simple. Helps viewers find more of you outside YouTube.

Tags note: Ramdy skips them. YouTube says tags play a minimal role unless something in your video title is commonly misspelled. Don't spend time on them.

---

### Part 4 — Upload checklist

Walk them through the YouTube Studio upload flow:

**Basic settings:**
- [ ] Title — final version from Part 2
- [ ] Description — from Underlord + any additional links
- [ ] Thumbnail — upload best option (or all 3 if A/B testing is available)
- [ ] "Made for kids?" → **No** (unless specifically children's content — marking incorrectly triggers content restrictions)
- [ ] Age restriction → No (unless applicable)
- [ ] Paid promotion → Check the box only if applicable; failing to disclose is a legal issue
- [ ] Allow automatic chapters → Yes (doesn't hurt to have as backup)
- [ ] Tags → Skip (Ramdy's call)
- [ ] Video language → English (or applicable)
- [ ] Category → Entertainment (or closest fit)
- [ ] Comments → On, basic moderation

**Subtitles:**
This is where the Descript SRT file comes in.
- In YouTube Studio → Subtitles
- Upload SRT file (select "With timing")
- This replaces YouTube's auto-generated captions with accurate, timed captions from your actual transcript

**End screens:**
Add once you have another video to point viewers to. For a first video, skip or leave blank.

**Cards:**
The circle-with-an-i pop-ups. Add later when there's related content to link to.

**Scheduling:**
Ramdy's approach: schedule rather than instant-publish. Gives you a buffer.
- Best time: Friday, 11:30 AM (Ramdy's choice — aligns with when audiences are active)
- Set the video as "Scheduled" not "Public" until the scheduled time
- Video should be completely done at least a day before scheduled posting

---

### The reality check (Ramdy's voice)

Before they hit publish, close with this:

> "Adrien said it well: optimization can only take a video so far. Good optimization helps a good video. It cannot save a bad one. If people click and immediately leave, YouTube notices and stops recommending it.
>
> So the strongest strategy isn't just optimizing each upload. It's consistently making videos people genuinely want to watch. Think of optimization as giving your video the best possible first impression — not as the thing that makes it succeed."

And then Ramdy's own attitude: keep making videos because you love it. If one blows up — great. That's not the reason you're doing this.

---

### Descript API — Retrieve published project metadata and subtitles

> The Descript API is early access and actively evolving. These skills describe **intent** — what to do and when. Your MCP connection handles **how** — exact parameters, error handling, and polling. If anything has changed, [docs.descriptapi.com](https://docs.descriptapi.com/) is the source of truth.

**When:** After the video has been published to a Descript web link (from the Export step in Episode 5).

**Operation:** `GET /published_projects/{publishedProjectSlug}`

The slug is the identifier at the end of the Descript share URL (e.g., `web.descript.com/abc123` → slug is `abc123`).

**What this returns:**

| Field | What to use it for |
|-------|--------------------|
| `download_url` | Direct download link for the exported video file |
| `metadata.title` | Confirm the project title |
| `metadata.duration_seconds` | Video length — useful for checking against YouTube's limits |
| `metadata.published_at` | Timestamp for your records |
| `subtitles` | Full transcript in **WebVTT format** — use this for YouTube captions |

**On subtitle format:** The API returns WebVTT (`.vtt`), not SRT (`.srt`). YouTube accepts both — you can upload the `.vtt` directly in YouTube Studio. If you need SRT specifically, convert it or export from the Descript app instead.

**This replaces the manual SRT export step** from Episode 5: if the video is published to a Descript link, subtitles can be fetched via API and handed directly to the upload flow without manual file export.

**If Descript MCP is not configured:** Export the SRT manually from the Descript export panel as described in Episode 5, then upload to YouTube Studio under Subtitles.

---

### Building the Upload entry

Add this to their Creator Profile:

```
## First Upload
[Added: Episode 6]

Final title: "[title]"
Thumbnail versions created: [1 / 2 / 3]
Description: [drafted via Underlord / written manually]
Subtitles: [SRT uploaded from Descript / pending]
Scheduled date: [date and time]
Publish URL: [add once live]

Upload checklist:
  [x] Title
  [x] Description
  [x] Thumbnail
  [x] "Made for kids?" → No
  [x] Subtitles uploaded
  [ ] End screens (add after second video)
  [ ] A/B thumbnail test (if eligible)
```

---

### Handoff to Episode 7

> "Your video is uploaded and scheduled. The hardest part is behind you.
>
> Now sit back and enjoy that wave of accomplishment for a minute. You made something that didn't exist before. There's not a lot of people who can say that.
>
> Okay. Now it's time to do it all over again — smarter and with a system.
>
> Episode 7 is about building a content calendar: how to stay consistent without burning out.
>
> Bring your Creator Profile and run:
>
> `/rcb-ep7-content-calendar`
>
> See you then, soldier."

---

## What this skill does NOT do

- It does not write your video title or description for you — it helps you find the best version of what you already have.
- It does not manage your YouTube Studio directly. You'll do that manually.
- It does not cover paid promotion, sponsorships, or YouTube monetization setup — those come with time.

---

## Source

Based on the transcript of [Ramdy Creator Bootcamp Episode 6 — "Optimizing Your Video"](https://www.youtube.com/playlist?list=PL0SvVPop_Y6zjqTAHCISdMGBQ1jPVv87S), featuring Adrien on YouTube strategy.
All core advice, philosophy, and framing belongs to Ramdy and Adrien.
