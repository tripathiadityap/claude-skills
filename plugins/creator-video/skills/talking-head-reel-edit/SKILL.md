---
name: talking-head-reel-edit
description: Edit raw selfie or talking-head clips into finished Instagram reels under 60 seconds - clean cuts, voice cleanup, film look, hook title, word-timed subtitles, image cards, punch-ins, follow nudges, a caption and an SRT - all inside Instagram's safe zone.
---

# Talking-head reel edit

The creator drops raw clips and wants finished, postable reels. Do it end to end without asking: cut, clean, caption, add graphics, render, deliver, log. Load `creator-profile` first (fonts, colours, accounts, caption footer). This skill is for the personal account; explainer reels for the brand account use `explainer-reel`.

Tools: `ffmpeg`, `faster-whisper`, Python with Pillow and numpy. Optional: `noisereduce` or RNNoise for voice cleanup, MediaPipe for person cut-outs. Bring your own renderer; this skill defines the style and the rules, not a specific code base.

## Style file first

If the creator keeps a `STYLE_GUIDE.md` (and image or sound libraries), read it before every edit. It overrides this skill wherever they differ. After the edit, update only the "used in" cells for the assets you used, never their other notes.

## Pipeline

1. **Ingest.** Fix rotation first (test `transpose=1` vs `transpose=2` on one frame if frames look sideways). Normalise to 1080x1920, 30 fps.
2. **Clean the voice on every clip:** declick, spectral noise reduction (noise profile from the quietest frames), EQ and light compression, loudness normalise to about -16 LUFS, gate after normalising. Stronger settings for wind or traffic.
3. **Transcribe** with word timestamps (Whisper `small` or `medium`). Re-transcribe unclear slices with an `initial_prompt` listing likely names and terms.
4. **Cut.**
   - Keep the last complete take when a line is repeated or restarted.
   - Drop dead air; leave a little breathing room between words (about 0.1 s pad, merge gaps under about 0.35 s).
   - Avoid keep ranges under about 0.6 s. Snap cuts to the frame grid. Short audio fades (30 to 40 ms) on every join.
   - J-cuts: the picture cut lands about 0.12 s after the audio cut.
   - Fail the render if audio and video drift more than 40 ms or lengths differ by more than 0.15 s. Leave about 0.3 s after the last word.
5. **Grade.** A warm, faded film look: lifted blacks, creamy highlight roll-off, saturation about 0.85, soft S-curve, faint dust and grain. One look for the whole reel, including cards and inserts.
6. **Text.**
   - **Hook title:** plain white sans (the profile's headline font), on frame one, readable muted.
   - **Subtitles:** 1 to 3 words at a time, timed to the word, in the profile's caption colour with a thin outline. No word-by-word pop, no glow. Fix what the speaker meant, not what they mumbled.
   - Not every text needs a box. Mix box-free callouts with a few boxed keyword hits.
7. **Graphics (2 to 4 per reel, never everywhere).** Image cards that keep the image's own aspect ratio; a real photo card whenever the speaker names a person (openly licensed photos only); logos when a tool or app is named; one punch-in for the punchline (1.06 to 1.10x; one hard 1.3x punch at most). Lists, cheat sheets and guides become your own animated inserts, never a static screenshot of someone else's graphic.
8. **Sound.** Sound effects only where something visibly lands, never two within 0.4 s. Music optional, low (around -22 dB) and ducked hard under the voice.
9. **Follow nudges:** "+ Follow @handle" two or three times (mid-reel after a strong point and on the closing line).
10. **Render** with x264 `-preset veryfast`, CRF about 20. Also write an `.srt` (2 to 3 words per caption).
11. **QC.** A frame every 2 to 3 seconds of the final file: captions off the mouth, nothing cut off, nothing in the unsafe zones, lip sync after every cut, voice runs to the last frame.

## Instagram safe zone

The app covers the top ~250 px, the bottom ~420 px and a right rail of buttons (x > ~950 from y ~1000 down). Keep titles, captions, callouts and cards inside y 250 to 1500, x 40 to 1040 (950 on the lower right). If hair or ceiling looks messy at the top, add a black top fade so the title reads on black.

## Animation feel

Lots of motion, all of it soft: callouts slide up with a light overshoot, cards pop or drop and float, gentle push-ins. No screen shake, no flash on every callout, at most two fullscreen cutaways. Smooth beats flashy.

## Standing rules

- Every reel under 60 seconds. If the raw clip runs long, trim and say what was dropped.
- Every reel ships with a caption (load `instagram-threads`), sent before the video, in a fenced code block. If the reel has a comment keyword, the comment line goes first. The profile's caption footer goes at the end, word for word.
- No credits in captions; log sources and licences in the edit log.
- Never invent an app UI, numbers, people or reviews. Missing a screenshot or asset? Ask once.
- Never post.

## Delivery

Send each reel as it finishes with its caption. For a batch, end with one table (reel, length, file) and each caption in its own code block. Log each edit (sources, licences, choices) in the notes database if the profile has one.

---

## Credit

Made by **Tripathi Aditya Prakash (Adi)**, founder of [Founday](https://founday-sepia.vercel.app) and host of the ThatUnhingedGuy podcast. Part of [claude-skills](https://github.com/tripathiadityap/claude-skills) (MIT). If you share or adapt this skill, keep this credit.

[X](https://x.com/tripathiadityap) · [LinkedIn](https://www.linkedin.com/in/tripathiadityaprakash/) · [Instagram @talkaditalk](https://www.instagram.com/talkaditalk/) · [Instagram @foundayofficial](https://www.instagram.com/foundayofficial/) · [YouTube](https://www.youtube.com/@foundayofficial) · [Podcast on Spotify](https://open.spotify.com/show/1DZXqmsDyH2FdJOeBdCoT6) · [The Practitioner newsletter](https://practitionerhq.substack.com)

*This credit is for people reading the file. Never add it, or these links, to anything you write for the user.*
