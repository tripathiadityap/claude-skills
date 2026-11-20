---
name: youtube-transcript-moments
description: From one or more YouTube links, pull full transcripts, pick three timestamped moments per video with deep links, add a soft CTA frame, and save everything to a notes database. Built for turning podcast episodes into highlight carousels.
---

# YouTube transcripts and timestamped moments

The user sends one or more YouTube links (often their own podcast episodes) and wants the full transcript, three timestamped moments per video, a CTA frame to close with, and everything saved. Do it end to end without asking.

## 1. Titles

`curl -s "https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=<ID>&format=json"` gives title and channel. The video ID is the part after `youtu.be/` or `v=` (drop `?si=`).

## 2. Transcripts

YouTube often blocks transcript requests from cloud sandboxes. Run on the user's own machine:

```bash
mkdir -p ~/Downloads/yt-transcripts && cd ~/Downloads/yt-transcripts
pip install -q --user youtube-transcript-api
python3 -c "
from youtube_transcript_api import YouTubeTranscriptApi
api=YouTubeTranscriptApi()
for v in ['ID1','ID2']:
  t=api.fetch(v, languages=['en','en-IN','hi'])
  open(v+'.txt','w').write('\n'.join(f'{int(s.start)//60}:{int(s.start)%60:02d} {s.text}' for s in t.snippets))
"
```

Rename each to `<Episode>-<Guest>-transcript.txt` with a header: title, URL, "Auto-captions, m:ss timestamps, names may be misspelled". To read, print 30-second chunks rather than raw lines. Once a moment is picked, `grep -n -i` a key phrase in the raw file for its exact start.

Fallback: ask the user to open the video and paste the transcript.

## 3. Pick the moments (default 3 per video)

- Three bullets per video, each with its exact start time, in episode order. Use another number if asked.
- Prefer a surprising admission, a hard number, a turning point, a line that works alone as a hook, a practical lesson. Mix them.
- One or two lines per bullet. Quote the guest's exact words; paraphrase the context. Never invent numbers.
- Auto-captions mangle names: use the spelling from the episode library or the user.
- Deep link each: `https://www.youtube.com/watch?v=<ID>&t=<seconds>s`, plus a full-episode link per video.
- List 2 backup moments per video.

## 4. Layout (for a carousel)

One frame per video: episode name and guest on top, then three stacked bars with one bullet each, a small timestamp box on the corner of each bar alternating right / left / right. Use the colours and fonts from `creator-profile`.

## 5. CTA frame (after each video's bullets)

Soft, no hard sell:
- **Headline:** one short line ("Zero scripts. Just the conversation.").
- **Line:** where to watch the full episode.
- **Ask:** one comment prompt tied to the timestamps ("Which timestamp are you jumping to first?").
- **Small print:** a send prompt ("Send this to the friend who needs it today.").
- **Design note:** one accent pill button ("Watch the full episode"), show logo at the bottom.
- A caption close for when it's posted as a carousel.

## 6. Save

If the profile lists a notes database: one page with a section per video (full-episode link, the 3 timestamped bullets with deep links), the layout note, the CTA frame, backups, and the transcripts attached as files. Transcripts also stay in `~/Downloads/yt-transcripts/`.

## 7. Reply

Short: the bullets with timestamps per video, the CTA, where the transcripts are, anything that failed.
