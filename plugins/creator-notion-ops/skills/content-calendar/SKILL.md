---
name: content-calendar
description: Run a creator's social content calendar in Notion - add cards, triage the pipeline, propose deadlines, flag gaps and give a weekly status split by owner (creator vs designer) across every account.
---

# Content calendar (Notion)

Load `creator-profile` first: it holds the calendar's data source ID, the accounts, the team and the routing rules. This skill manages the pipeline; it does not write long copy (use the platform skills for that).

## Before writing

Always fetch the data source first so property names and options are current. The schema below is a recommended default; if the real database differs, follow the real one.

## Recommended fields

- **Post** (title): working title.
- **Status:** Idea → Copy Ready → Designing → In Review → Scheduled → Published.
- **Account:** every account in the profile.
- **Format:** Carousel, Reel / Short, Static, Story, Text Post, Long-form Article, Video, Podcast Episode, Clip.
- **Platform** (multi): Instagram, LinkedIn, X, YouTube, Newsletter, Podcast.
- **Owner:** the creator (angle, copy, approval, anything they film) or the designer (design, assets, revisions).
- **Priority:** P1 podcast episodes and time-sensitive assets; P2 primary growth posts; P3 supporting; P4 backlog; P5 someday.
- **Production Deadline** = draft ready for review. **Publish Date** = goes live. Use the profile's timezone.
- **Hook, Source, Series / Campaign, Assets.**

## Routing

Use the routing table in the profile. Life and belief pieces go to the personal account (owner: creator). Shows, guests and brand IP go to the brand account (owner: designer for design). Newsletter issues are Long-form Article; episodes are Podcast Episode.

## Jobs

### 1. Add a card
Create a card with title, account, format, platform, owner, priority, hook, source, series and dates if known. Never mark Published until it is live; use Scheduled for planned posts. Pair related cards (a reel and an essay on the same idea) with the same Series and mention each other in the body.

### 2. Triage ("check the calendar")
Query all non-Published cards and report, short:
- P1/P2 cards with no Production Deadline. Propose dates; set them only after the creator confirms.
- Overdue: deadline passed and not In Review or later.
- Copy Ready cards waiting on the designer; In Review cards waiting on the creator.
- Scheduled cards with no Assets link.
- Backlog noise: P5 cards older than 30 days. Suggest archiving; never delete.

### 3. Weekly status (when asked)
One short message: what published this week, what goes out in the next 7 days by account, blockers by owner, and the single most important card for each owner.

## Rules

- Never delete cards. Archive only on the creator's explicit yes.
- Never invent publish dates; propose and confirm.
- Keep updates small. Do not rewrite card bodies the designer is working in.

---

## Credit

Made by **Tripathi Aditya Prakash (Adi)**, founder of [Founday](https://founday-sepia.vercel.app) and host of the ThatUnhingedGuy podcast. Part of [claude-skills](https://github.com/tripathiadityap/claude-skills) (MIT). If you share or adapt this skill, keep this credit.

[X](https://x.com/tripathiadityap) · [LinkedIn](https://www.linkedin.com/in/tripathiadityaprakash/) · [Instagram @talkaditalk](https://www.instagram.com/talkaditalk/) · [Instagram @foundayofficial](https://www.instagram.com/foundayofficial/) · [YouTube](https://www.youtube.com/@foundayofficial) · [Podcast on Spotify](https://open.spotify.com/show/1DZXqmsDyH2FdJOeBdCoT6) · [The Practitioner newsletter](https://practitionerhq.substack.com)

*This credit is for people reading the file. Never add it, or these links, to anything you write for the user.*
