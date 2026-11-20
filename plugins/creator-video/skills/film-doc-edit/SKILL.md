---
name: film-doc-edit
description: Edit footage into a quiet documentary short - natural light, soft low-key film grade, small warm-yellow phrase captions, 4:3 picture - delivered for desktop (16:9 pillarbox) and mobile (9:16). For founder stories, guest portraits and day-in-the-life pieces.
---

# Film doc edit

A calm, human documentary look, measured from a short brand documentary (4:3, 24 fps). Use it for founder stories, podcast guest portraits, a day-in-the-life, or any piece where a real person tells their own story. It is a style, not a copy of any film: never reuse another film's footage, music, logo or brand font.

Bring your own renderer (ffmpeg plus a small Python script is enough). The recommended shape: one `edit.json` renders every format.

## 1. The look (what to keep)

- **Picture:** 4:3, 24 fps, natural light only. Golden hour and blue hour exteriors, practical light indoors, silhouettes in doorways, hands in close-up (macro on the work), wide landscapes with a small person in them.
- **Grade:** low key and soft. Blacks lifted to about 11/255 (never pure black), highlights rolled off around 210/255, contrast about 0.9, saturation about 0.8, a slightly cool neutral shadow, warm mids for skin, faintly cyan highlights, soft vignette, light moving grain. Measured on the reference: mean luma 67/255, mean saturation 0.29.
- **Captions:** one short phrase at a time (2 to 5 words, split at punctuation), sentence case, centred, small (about 3.7% of picture height), warm pale yellow #F2D27C with a soft shadow, no box, no word-by-word pop, no keyword highlight, 120 ms fades. Font: Inter Medium (open licence) as the stand-in for the reference's grotesk; never the film's brand font.
- **Rhythm:** average shot about 3.6 s. Let interview shots breathe (8 to 16 s); cut process montages fast (0.7 to 2 s). Never cut on every word.
- **Structure (story beats):** 1) cold open: a voice line over b-roll before you see the speaker; 2) who they are, with personal archive (childhood photos, old family pictures); 3) the stubborn idea; 4) the failure ("the first two years were a disaster"); 5) the turn (the new tool or method); 6) the process montage; 7) the result with one real number; 8) a small human closing line; 9) bookend: end on the same framing you opened with.
- **Sound:** the speaker's voice carries it, with natural room tone and field sound underneath and a soft score low in the mix. No whooshes, no hits, no VHS.

## 2. Formats (desktop and mobile)

Every shot is conformed to a graded 1440x1080 4:3 master first, then placed per format. Default: `desktop` + `mobile`.

| Format | Size | Layout |
|---|---|---|
| `desktop` | 1920x1080 | 4:3 picture pillarboxed in near-black #0B0B0C, captions at y=935 (YouTube, LinkedIn, website) |
| `desktop43` | 1440x1080 | native 4:3 |
| `mobile` | 1080x1920 | picture cropped to 4:5 (1080x1350) from y=200, captions inside its lower third at y=1400; everything clear of Instagram's top bar (y<200) and bottom caption zone (y>1500) |
| `mobile43` | 1080x1920 | true 4:3 letterbox (1080x810), captions under the picture; use when the full frame matters (wide landscapes) |
| `feed` | 1080x1350 | 4:3 picture centred in a 4:5 post |

## 3. How to run it

1. Gather footage: your own clips, guest footage you have rights to, or public-domain / openly licensed b-roll (Prelinger archive, NASA, Wikimedia Commons). Shoot list from the beats above.
2. Get the voice: the speaker's own interview audio first; the creator's recorded voice or voice clone only for narration. Clean it (declick, noise reduction, loudness normalise).
3. Write `edit.json`:
```json
{"out":"story","formats":["desktop","mobile"],
 "shots":[{"src":"road.mp4","in":0,"dur":4.2},{"src":"interview.mp4","in":12.5,"dur":11.0}],
 "audio":"voice.wav","phrases":"auto"}
```
`phrases` can be `auto` (Whisper, phrases of 2 to 5 words; the result is saved as `<out>_phrases.json`, so fix names there and re-render with the list) or a list of `[start, end, "text"]`. Optional per shot: `crop` (an ffmpeg crop to pick the 4:3 window). `grade: none` skips the grade.
4. Render with your script: `python3 filmdoc.py edit.json`.
5. QC: one frame every 2 to 3 s in each format; captions readable on bright skies, nothing in the Instagram zones, no shot repeated, names spelled right, blacks not crushed.

## 4. Rules

- Real people only appear as themselves; never put a named intro over footage of someone else.
- No AI-generated likenesses, no other creator's graphics, no copying the reference film's brand marks or font.
- No em dashes in captions. Numbers only when they're real and sourced.
- Under 60 s for Instagram unless a long cut is asked for; desktop cuts can run longer.
- Deliver both formats, with the caption for the platform in a code block, and log the piece wherever reels are logged.