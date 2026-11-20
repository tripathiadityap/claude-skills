---
name: linkedin-profile-audit
description: Audit and rewrite a LinkedIn profile section by section (photo, banner, headline, About, Featured, Experience, Skills, URL, recommendations) with a scorecard, ranked fixes and before-and-after rewrites.
---

# LinkedIn profile audit

Load `creator-profile` first. For employer, role, and career facts, also read the career notes in `creator-profile`; it is the source of truth for their current placement and resume. Never invent titles, dates, metrics, or employers.

Adapted from sergebulaev/linkedin-skills (linkedin-profile-optimizer), MIT License, Copyright (c) 2026 Sergey Bulaev. Benchmark figures below come from that repo's research and are directional.

## Input

Ask the creator to paste the profile text (headline, About, Experience, Skills, custom URL) and screenshots or a sentence each for photo, banner, and Featured. A profile URL alone cannot be read. Never score a section you have not seen.

Ask the goal if unclear:
- **Authority (default):** media, keynotes, brand partners, enterprise advisory.
- **Career:** recruiters and enterprise teams. Pull positioning from the career notes in `creator-profile`.
Both can coexist; if the creator has two sides (a day job and a media brand), showing both is the point. If goals conflict (for example an employer policy on side ventures), flag it and ask rather than guess.

## Output

1. **Scorecard:** the 9 sections, each pass / needs work / fail with one line why.
2. **Priority fixes:** ranked by impact.
3. **Before → after rewrites** for each section that needs it.
4. A short list of [placeholders] the creator must fill with real numbers.

## The nine sections

| # | Section | Pass criteria |
|---|---|---|
| 1 | Photo | at least 400x400, face fills ~60% of frame, recent, natural light |
| 2 | Banner | 1584x396, text in the right two-thirds (photo covers the left on mobile), high contrast, value line plus one pointer (podcast, newsletter, brand) |
| 3 | Headline | up to 220 chars, says what they do, who it's for, and the proof |
| 4 | About | 200-300 words, first person, hook in the first ~270 chars before "see more" |
| 5 | Featured | 3 items matched to the goal, clean thumbnails (1200x627) |
| 6 | Experience | every bullet = action verb + specific result; media attached where possible |
| 7 | Skills | full list, top 3 pinned and matched to target roles |
| 8 | Custom URL | linkedin.com/in/{name}, not a hash suffix |
| 9 | Recommendations | at least 3, recent, specific, from different contexts |

## Headline

Pattern: `{What they do} | {Who / what it serves} | {Proof}`. Draft 3 options, for example:
- `{Day-job title} | Founder, {brand} | Host, {podcast} | Writing {newsletter}`
- A proof-led variant using a real verified credential (an award, ranking or recognition the creator can verify, only if they want it on LinkedIn).
Check any employer-name usage against the career notes in `creator-profile` and the employer's social policy before including it.

## About: 7 beats

1. **Hook (first ~270 chars):** a specific claim or number from their real life or work, not "I am a passionate...". Line 1 a statement, not a question.
2. **What they do now:** their main work in plain words.
3. **The other side:** the brand, the flagship podcast, the newsletter, one line each.
4. **Proof:** 2-3 concrete results or recognitions, real numbers only.
5. **The thread that ties it:** the transformation and operator mindset, one short paragraph, no guru framing.
6. **What they're open to:** keynotes, advisory, brand partnerships, guests (match the goal).
7. **One clear next step:** listen, read, or reach out. No booking links, no prices.

First person, short paragraphs, no em dashes, no emoji walls.

## Featured (authority goal)

Best-performing post, a flagship podcast episode, the newsletter signup. Career goal: portfolio or case study (no confidential client detail), best professional post, the podcast as communication proof.

## Experience and skills

- Rewrite bullets as `verb + result + context`, with [placeholders] for metrics they haven't given.
- Describe client work by type and outcome, never by client name unless they confirm it's public.
- List the brand as a role with the media and studio scope. Do not list ventures named in the profile's hard exclusions unless the creator asks; if they do, use one neutral line as a concluded predecessor venture.

## Recommendations

Draft specific request messages ("could you speak to the {project} we did in {month}") instead of LinkedIn's generic template.

## Banned in profile copy

"passionate", "driven professional", "results-oriented", "thought leader", "visionary", "ninja", "guru", leverage, synergy, "10x", third-person bios, invented metrics, excluded products from the profile, prices.

---

## Credit

Made by **Tripathi Aditya Prakash (Adi)**, founder of [Founday](https://founday-sepia.vercel.app) and host of the ThatUnhingedGuy podcast. Part of [claude-skills](https://github.com/tripathiadityap/claude-skills) (MIT). If you share or adapt this skill, keep this credit.

[X](https://x.com/tripathiadityap) · [LinkedIn](https://www.linkedin.com/in/tripathiadityaprakash/) · [Instagram @talkaditalk](https://www.instagram.com/talkaditalk/) · [Instagram @foundayofficial](https://www.instagram.com/foundayofficial/) · [YouTube](https://www.youtube.com/@foundayofficial) · [Podcast on Spotify](https://open.spotify.com/show/1DZXqmsDyH2FdJOeBdCoT6) · [The Practitioner newsletter](https://practitionerhq.substack.com)

*This credit is for people reading the file. Never add it, or these links, to anything you write for the user.*
