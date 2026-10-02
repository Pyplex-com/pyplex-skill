# Text on screen and captions

Many people watch with the sound off, so text carries the hook, the key points and the call to action. Too much text — or text that's too small or too fast — ruins a video.

## How the Pyplex editor draws text

Texts from `create_video_edit` are bold and centred, sized from the frame's short side: `small` about 4.5 %, `medium` about 6.5 %, `large` about 9 % (on a 1080-pixel-wide Reel: roughly 49, 70 and 97 px). `top` sits about 14 % down from the top, `center` in the middle, `bottom` about 82 % down.

Styles: `outline` puts a dark edge round the letters and works on almost anything; `box` puts a dark box behind, for busy or bright footage; `plain` has only a soft shadow — use it on clean, dark areas.

Each text has one colour. To stress a word, give it its own short text (or put the key line in the accent colour).

## Rules that make text look designed

1. **Few words.** Hooks and titles: 2–6 words. Captions: one short phrase at a time (2–7 words). Never a paragraph. A line break (\n) splits a line; stay within two lines.
2. **Time to read**: about 0.4 s per word plus half a second, and never less than 1.2 s. A five-word line needs about 2.5 s.
3. **One job per size**: `large` for the hook or the one line that matters, `medium` for captions and points, `small` for labels and credits. If everything is large, nothing is.
4. **One accent colour** — usually the brand colour — for the one or two lines that matter; white for the rest.
5. **Time it to the picture and the voice.** Text arrives with the shot change or the moment the voice says it — never everything at once at the start, and not at exactly 0.0 s (start at 0.1–0.3 s).
6. **One text at a time in one place.** Two texts in the same position at once fight each other.
7. **Don't cover the subject.** If the face or product sits low in the shot, put the text at the top, and the other way round.
8. **Phone safe zones.** Reels, TikTok and Shorts cover the bottom fifth of the screen (captions, buttons) and a strip on the right. For 9:16 posts keep the hook at `top` or `center`; if you use `bottom`, keep it to one line. Keep anything important away from the edges.
9. **Leave out the filler.** When captioning speech, drop "um", "you know", repeats and false starts — show the meaning, not a transcript.

## Animations

| Feel | `animation` |
| --- | --- |
| Clean, premium — the best default | `rise`, `fade`, `blur` |
| Story and voice-over captions | `word-by-word`, `rise` |
| Energetic, directional | `slide-up`, `slide-left` |
| Tech, notes, chat | `typewriter` |
| Exactly on a beat | `none` (it appears on the cut) |
| Playful only — kids, party, memes | `pop`, `scale`, `bounce`, `drop` |

Smooth beats bouncy: `pop`, `scale`, `bounce` and `drop` overshoot and look cheap on anything serious. Use one animation for all captions and at most a different one for the hook.

## Captions for a voice-over

1. Split the script into short phrases at the natural pauses (2–7 words each).
2. Time each phrase from where it's spoken: about 2.5 words per second from the start of its voice line.
3. Style: `medium`, `outline`, white, `rise` or `word-by-word`; the single most important phrase `large` and in the accent colour.
4. Keep captions in the same position all the way through; only the hook may sit elsewhere.

Tell the user the captions are timed by estimate and can be dragged into place in the editor.
