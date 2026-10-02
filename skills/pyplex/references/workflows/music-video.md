# A video cut to music

Montages, travel videos, event highlights, lyric-style videos, brand moods — the music drives every cut.

Read first: [pacing](../craft/pacing.md), [sound](../craft/sound.md), [transitions](../craft/transitions.md).

## 1. The music comes first

- **The user's track**: `request_upload_link` (kind "audio"). You can't hear it, so ask for its BPM or where the drop or chorus comes.
- **A new track**: `elevenlabs/music-v2.5` with the genre, the BPM, the structure with timings ("soft intro 0–4 s, build 4–8 s, drop at 8 s, outro from 20 s") and a length of the video plus 2 s.
- Decide which kind it is:
  - **Rhythmic** (a clear beat): cut on the beats.
  - **Calm** (no strong beat): change shots every 4–6 s on the phrases, with slow zooms and soft transitions.

## 2. Map the cuts

A beat lasts 60 ÷ BPM seconds. Lay out a grid and place the shots on it:

| Part | Seconds (at 120 BPM) | Cut every | Shots |
| --- | --- | --- | --- |
| Intro | 0–4 | 4 beats (2 s) | 2 wide, calm shots |
| Build | 4–8 | 2 beats (1 s) | 4 medium shots, getting faster |
| Drop | 8–16 | 1 beat (0.5 s) | the best, most energetic shots |
| Outro | 16–20 | 8 beats (4 s) | 1 slow wide shot; the title or logo |

The strongest shot lands on the drop. Very short shots need strong, simple images — action, colour, faces.

## 3. Shots

- The user's photos and clips (up to 10 files per upload link — make another link for more).
- AI clips: 4 s each is plenty, because you'll use only 0.5–2 s of each — pick the best moment with `trim_start`. One 4-second clip can even give two or three different short cuts: use the same source again with another `trim_start`.
- Photos: alternate `motion` "zoom_in" and "zoom_out", so stills move with the music.

## 4. Text

- Lyric-style: one line per musical phrase, on screen for at least a full beat — usually 1.5–3 s — with `word-by-word` or `fade`.
- Montage: a title at the start and one line at the end, both on the beat.

## 5. Mix

Music at 0.8–0.9 with a `fade_out` of 1.5–2 s (or end exactly on the final hit). Clips at `volume` 0 unless a clip's own sound is part of the moment — a cheer, a splash.
