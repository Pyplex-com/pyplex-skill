# Music, voice and sound

Sound decides how a video feels. Viewers forgive an average shot; they leave on bad sound.

## Decide what leads

- **Music-led** (montages, ads without speech, travel, products): choose or make the music first — its tempo sets the cuts ([pacing](pacing.md)).
- **Voice-led** (explainers, stories, tutorials): write and make the voice-over first — its length sets the timing of every shot and caption.
- **Natural sound** (a sizzling pan, rain, a busy street): keep the clips' own sound and add soft music under it, or none.

## Making music

`elevenlabs/music-v2.5` gives the most control: a `prompt`, the exact length in `music_length_ms` (3000–600000), and `force_instrumental` for no vocals. Also good: `google/lyria-3-pro/music`, and `hosted/ace-step-1.5` for a song with your own `lyrics`.

Prompt recipe — genre, mood, tempo, instruments, shape, ending:

> Upbeat lo-fi house, 118 BPM, warm keys and soft plucked bass, bright and friendly, a 2-second intro, a clear lift at 8 seconds, ends on a clean final hit, instrumental.

- **Make it 2–3 seconds longer than the video**, so it never runs out early, and fade it out.
- **Ask for a short intro** in short videos — a long build-up wastes the first seconds. If a track still starts slowly, use the audio's `trim_start` to begin at a stronger part.
- Name a **BPM** when you plan to cut on the beat, and name the ending ("ends on a final hit", "fades out softly").
- Instrumental under a voice — sung words fight spoken words.
- Don't imitate a named artist or a famous song. If the user wants their own licensed track, they upload it (`request_upload_link`, kind "audio") or add it in the editor.

## Voice-over

`elevenlabs/eleven-v3` (expressive) or `elevenlabs/multilingual-v2` (many languages, such as Hindi or Spanish). The words go in `text`; keep the default `voice_id` unless the user asks for another voice.

- Write for the ear: short sentences, the way people talk, about 2.5 words per second.
- One voice file per section (hook, middle, ending) makes timing easier — each starts where its section starts. An edit takes up to 5 audio tracks: the music plus up to 4 voice parts.
- Never clone or imitate a real person's voice without their permission (Pyplex rules).

## Sound effects

A whoosh on a fast transition, an impact on a reveal, a shutter click on a photo — small sounds make an edit feel expensive.

- From a description: `mirelo-ai/sfx-1.6/text-to-audio` (the description goes in `text_prompt`) or `sonilo/v1/text-to-sfx`.
- Sound for a silent clip, matched to what happens in it: `hosted/mmaudio-v2`, `mirelo-ai/sfx-1.6/video-to-video` or `kwaivgi/kling-video-to-audio`.
- Use them sparingly: three well-placed effects beat thirty.

## Mixing in the edit

| Track | `volume` | Fades |
| --- | --- | --- |
| Music on its own | 0.7–0.9 | `fade_in` 0–0.5 s, `fade_out` 1–2 s |
| Music under a voice | 0.15–0.3 | the same |
| Voice-over | 1.0 | none |
| The AI clips' own sound, under music | 0 (or 0.2–0.4 for real ambience) | — |
| Sound effects | 0.5–0.9 | none |

- The music ends with the video: a fade-out over the last 1–2 s, or the music's final hit on the last frame.
- A moment of silence right before the drop or the reveal makes it hit harder.
