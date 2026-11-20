---
name: second-brain-daily
description: Route anything the user shares about their day into the right Notion Second Brain database - quick capture, daily notes, knowledge library, meeting notes, weekly reviews or decisions - in under three lines of output.
---

# Second Brain daily updater

When the user chats about their day, ideas, learnings, meetings or decisions, detect what it is and log it in the right Notion database with zero friction.

Triggers: "log this", "add to notion", "capture this", "quick thought", "I had a meeting", "I learned", "today was", morning or evening check-in, "weekly review", a decision about their venture. If they casually mention something worth keeping, offer once to log it.

## The six databases

Data source IDs live in `creator-profile` (Tools section). If they are missing, ask once and suggest adding them there.

| Database | When |
|---|---|
| Quick Capture (default) | Fleeting thoughts, "I should...", ideas, links, questions, "what if" |
| Daily Notes | Explicitly about today: energy, what got done, top 3 wins. One per day |
| Knowledge Library | Learned from a source: article, video, podcast, book, a conversation that changed their thinking |
| Meeting Notes | Someone else was involved: client, guest, collaborator, sponsor, mentor |
| Weekly Reviews | Sunday, or "weekly review". Has numbers (followers, revenue, content count, plays, subscribers) |
| Decisions | A clear decision about the venture: product, content, partnerships, hiring, pricing, strategy |

If it doesn't clearly fit, it goes to Quick Capture.

## Field mapping (recommended schema; follow the real one if it differs)

- **Quick Capture:** Thought (title, verbatim or lightly cleaned) · Type: Idea / Task / Resource / Question / Insight / Other · Date · Status: Raw
- **Daily Notes:** Date (title, "Mon, 18 May 2026") · Day · Energy 1-5 (default 3) · Top 3 Done · Content Idea Captured · Week (ISO number)
- **Knowledge Library:** Title · Type: Article / Video / Book / Podcast / Conversation / Course / Other · Topic tags · Big Idea (1-2 sentences) · Date
- **Meeting Notes:** Meeting ("Call with [Name] re [Topic]") · Date · With · Format: Call / In-Person / DM · Type: Client / Collab / Investor / Mentor / Internal / Other · Key Insight · Action Items
- **Weekly Reviews:** Week ("Week 21: Mon 18 May to Sun 24 May 2026") · Date (Sunday) · Revenue · New Followers · Content Published · Top Win · What Didn't Work · Next Week Focus
- **Decisions:** Decision · Date · Status: Made · Area: Product / Marketing / Content / Operations / Hiring / Finance · Impact: High / Medium / Low · The Why (1-3 sentences)

Fetch the data source before the first write of a session so property names and options match.

## Behaviour

1. **Detect** which database fits.
2. **Confirm briefly** (optional): "Logging to Quick Capture as Idea, cool?" Skip if they say "just log it".
3. **Create the entry** with the data source as parent.
4. **Confirm done** in one line with a link.

Keep the whole exchange under three lines. Use today's date from the system context (YYYY-MM-DD for date fields).

Good: `Quick Capture → Idea logged. [link]`
Bad: "I've successfully added your thought to the Quick Capture database in your Notion Second Brain! Here's a summary..."
