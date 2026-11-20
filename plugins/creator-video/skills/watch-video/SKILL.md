---
name: watch-video
description: Watch a reel, YouTube video, Short or X video from a link - download it, transcribe locally with Whisper, make a contact sheet of what is on screen, and report the hook, structure beat by beat and how to apply it. Runs on the user's own machine.
---

# Watch a video

The user sends a video link (Instagram reel, YouTube, Shorts, X) and wants it watched. Do it end to end without asking.

## Where to run

Cloud sandboxes are usually blocked by YouTube and Instagram, so run on the user's own machine (local shell, or a connected device tool). Work in a scratch folder such as `~/Downloads/watch/`.

Tools needed (install only if missing, with the user's OK):

```bash
pip install --user -U yt-dlp faster-whisper
# ffmpeg from your package manager, e.g. brew install ffmpeg
```

Optional: [Agent-Reach](https://github.com/Panniantong/Agent-Reach) (MIT) for wider platform coverage. Install it from GitHub only, never a same-named package from PyPI, and never run its system-wide installer unless the user asks.

## 1. Download

```bash
mkdir -p ~/Downloads/watch && cd ~/Downloads/watch
yt-dlp -f "best[height<=720]/best" -o "%(extractor)s_%(id)s.%(ext)s" "URL"
yt-dlp --dump-json --skip-download "URL" > meta.json   # title, uploader, caption, duration, views
```

For long YouTube videos, skip the video and pull captions instead:
`yt-dlp --write-sub --write-auto-sub --sub-lang en --skip-download --sub-format vtt -o "yt_%(id)s" "URL"`.
For timestamped highlights from a podcast, use `youtube-transcript-moments`.

## 2. Listen

No usable captions (reels never have them): transcribe locally.

```bash
ffmpeg -loglevel error -y -i VIDEO -ac 1 -ar 16000 audio.wav
python3 -c "
from faster_whisper import WhisperModel
m=WhisperModel('base',device='cpu',compute_type='int8')
segs,_=m.transcribe('audio.wav')
for s in segs: print(f'{int(s.start)//60}:{int(s.start)%60:02d} {s.text.strip()}')
" > transcript.txt
```

Use the `small` model for non-English, mixed-language or noisy audio. Do not send audio to a cloud transcription API unless the user says so.

## 3. Look

One contact sheet so on-screen text, framing, cuts and b-roll get seen:

```bash
ffmpeg -loglevel error -y -i VIDEO -vf "fps=1/3,scale=360:-1,tile=4x2" -frames:v 1 contact.jpg
```

Use `fps=1` for reels under 20 s, `fps=1/10` for long videos. Open the image. Also grab frame 0 alone if the hook text matters.

## 4. Report what was asked

Default: who and what; the hook (on-screen text and first spoken line, word for word); the structure beat by beat with timestamps; what makes it work; how it could apply to the user's own pages. If they ask to recreate it, use `instagram-threads` and `creator-profile`.

Quote only what was actually said or shown. Never invent numbers. Never post anything.

## 5. Save (if the profile lists a notes database)

One page per video: title, link, creator, transcript, on-screen text, breakdown, the user's version if made.

## Limits

- Private, login-only or story content can't be fetched anonymously. Ask for a screen recording instead.
- On a login wall or HTTP 429, wait and retry once, then ask for the file.

## Reply

Short: the hook, the 3 to 5 things that matter, and where the notes were saved.
