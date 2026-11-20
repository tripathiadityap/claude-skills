---
name: explainer-reel
description: Make fact-checked "real story" explainer reels under 60 seconds for a brand account - the viral claim vs the original source, voice-over, archival b-roll, licensed photos, quiet paper cards, signature keyword styling and a comment-keyword CTA.
---

# Explainer reel ("the real story")

For the brand account only. Talking-head clips and reels about the creator's own life go to `talking-head-reel-edit`. Load `creator-profile` first (voice clone ID, colours, fonts, signature device, caption footer). If it isn't clear which account a reel is for, ask once before building.

## The angle: context is the twist

Check the viral claim against the original source. The gap between what the clip says and what was actually said is the story (a clip says "every single day", the original interview says "nearly every day"). Reported vs confirmed stays explicit. Never state an allegation as fact.

Skip controversial angles even when the facts check out: no stories tying a living person to weapons, disasters or scandals, no predictions of someone's downfall, no political or culture-war takes.

## Rules that never bend

- **Under 60 seconds.** About 110 to 120 words of voice-over, 8 to 11 shots. Spliced source audio counts toward the 60 s.
- **Minimal.** Footage first. At most one info card of text, one short hook title on the first shot, tiny credits.
- **Signature keywords.** The 5 to 8 words that carry the story get the profile's signature device (for example a bold italic word in the accent colour between tall thin brackets). Everything else is small, plain captions.
- **No repeats.** Never show the same photo or clip framing twice. The last shot before the end card is always new. Short on images? Use a number card, comparison card or typographic card, not a repeat.
- **Real numbers only.** A date, number or place you couldn't verify stays vague ("once", "about") and you tell the creator which.
- **Openly licensed images only** (Wikimedia Commons, public-domain archives, NASA). Credits in the edit log, never the caption. Never AI lookalikes of real people.
- **Third-party clips:** 3 to 5 s, only when they really add; crop off anyone else's burned-in captions; flag the copyright risk.
- Never post. Never print an API key.

## Pipeline

1. **Source.** Pull the clip (`yt-dlp`), transcribe (`faster-whisper`), find the original interview, article or filing.
2. **Script.** Hook (the viral claim or a question) → who and what → what the original source says → the brand's take → the CTA line. Fact-check every number on its source page.
3. **Voice.** The creator's own recording first (clean it, Whisper for word timings). Otherwise the voice clone from the profile (e.g. ElevenLabs with timestamps), API key kept in an environment variable, never in files or chat.
4. **Images and b-roll.** A new shot every 1 to 2.5 s matching the phrase being said: the speaker's clip for their lines, archival b-roll for ideas, real photos for names, paper cards for studies and numbers. Check every archive clip for title cards, logos and off-topic frames before using it.
5. **Build and render.** Shots anchored to word timings. Film pass on everything (warm faded grade, grain, slight gate weave). x264 `-preset veryfast`.
6. **QC.** Under 60 s; frames at the hook, a keyword, the end card; then a full-size frame every 2 to 3 s: no repeats, no archive title cards, nothing cut off, white text never on a bright photo without a darkened zone or outline.

## Paper cards (quiet typographic shots)

Alternate footage with 2 to 4 cards on a light paper background (#F3F1EC with a soft vignette and grain, ink text), one idea per card, lots of empty space: one giant word or number alone; a short sentence with one word in italic serif in the accent colour; a small centred photo tile with a tiny caption; a simple ring chart comparing two real numbers; an article screenshot with a marker sweep on the key line. Words arrive one at a time on the voice.

## Other formats (pick by the reference the creator sends)

- **Interview or stage clip:** clip audio plus voice-over over photos and cards.
- **Stick-figure doodle:** drawn on the brand's dark background, one drawing idea per sentence, each item timed to the word. Book covers are your own drawn covers, never the real art.
- **Science look:** real black-and-white imagery in a soft-masked window, one highlight per shot, thin ring, small mono labels with leader lines, a big number with its citation. Drawn networks are labelled "Illustration, not real data".

## CTA

One comment keyword on every reel (e.g. STORY). Voice-over last line: "Follow along, and comment STORY for all the notes." End card: the wordmark and handle plus the keyword line. The DM that answers the keyword links a public notes page with the claim, what's true, the brand's take and source links; add an entry there after every reel.

## Caption

Hook line, 2 to 3 short paragraphs with the real source, one specific send or save CTA, then the profile's brand caption footer word for word. Three reel-specific hashtags at the front of the footer's hashtag line.

## Delivery

Say up front roughly how long the batch will take. Send each reel as soon as it finishes, with its caption in a code block. Several links in a row are a queue: make them all, in order. End a batch with one table (no., reel, length, file). Log every reel (number, title, length, format, source link, voice, photo credits, facts still to check) in the notes database if the profile has one.
