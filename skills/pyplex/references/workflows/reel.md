# Reel, TikTok or Short

A 9:16 video of 10–30 seconds, made to stop the scroll — from an idea ("a Reel for my café"), from the user's own photos and clips, or both.

Read first: [story](../craft/story.md), [shots](../craft/shots.md), [pacing](../craft/pacing.md), [text](../craft/text.md).

## 1. Brief — one message

Ask only what you can't decide: what it's for (sell, show, entertain), what must be in it (their face, product, place, logo, exact words) and a budget if it needs several AI clips. Your defaults: 9:16, 15–20 s, instrumental music, short on-screen text.

## 2. The plan — one message, before anything is paid for

- **Idea** in one line, and the **hook**: what happens in the first second.
- **Beats**: 6–10 shots of 1–3 s each, in a beat sheet.
- **Shots**: for each, the user's photo or an AI clip, the model, its length and its start image.
- **Text**: the hook line, 2–4 short captions, the call to action.
- **Music**: style, BPM and length (video + 2 s), or the user's own track.
- **Transitions**: one style — for example hard cuts on the beat and `zoomBlur` into the hero shot.
- **Price**: each AI piece from `get_price`, the total, and the export fee.

## 3. Make the pieces

1. Their photos and clips: `request_upload_link` (kind "any", up to 10 files) → `check_upload`.
2. Keyframe images in 9:16 first — cheap, and the clips are made from them.
3. Animate the keyframes with `bytedance/seedance-2.5/image-to-video`, 4–5 s each, with the camera moves from the shot list.
4. Music: `elevenlabs/music-v2.5` with `force_instrumental` on and the length set to the video plus 2–3 s.

The user's one yes to the plan covers all of these: quote each one and start it straight away, without asking again (the money rule in SKILL.md).

## 4. Build the edit

Example with 120 BPM music (a beat is 0.5 s; cuts every 2 or 4 beats, then two slower closing shots):

```json
{
  "title": "Cold brew reel",
  "aspect_ratio": "9:16",
  "clips": [
    { "source": "generation:<ice>", "trim_start": 0.5, "duration": 1, "volume": 0 },
    { "source": "generation:<pour>", "trim_start": 0.6, "duration": 1, "volume": 0 },
    { "source": "generation:<barista>", "trim_start": 0.5, "duration": 2, "volume": 0 },
    { "source": "upload:<upload_id>:1", "duration": 2, "motion": "zoom_in", "transition": { "type": "zoomBlur", "duration": 0.3 } },
    { "source": "generation:<hero>", "trim_start": 0.4, "duration": 3, "volume": 0, "transition": { "type": "dipToBlack", "duration": 0.6 } },
    { "source": "generation:<cafe-front>", "trim_start": 0.5, "duration": 3, "volume": 0 }
  ],
  "texts": [
    { "text": "Hot outside?", "start": 0.2, "duration": 1.6, "position": "center", "size": "large", "animation": "rise" },
    { "text": "Our cold brew fixes that", "start": 2.1, "duration": 1.8, "position": "top", "size": "medium", "animation": "rise" },
    { "text": "Open till 11 pm", "start": 9.1, "duration": 2.8, "position": "center", "size": "large", "color": "#FFD400", "animation": "fade" }
  ],
  "audio": [
    { "source": "generation:<music>", "volume": 0.85, "fade_out": 1.5 }
  ]
}
```

The clips start at 0, 1, 2, 4, 6 and 9 s, so the video is 12 s long. The `zoomBlur` sits on the user's photo because a clip's transition is the effect into the next clip — here, the hero shot. The last text lands on the last shot.

## 5. Hand over

Send the Open in Editor link with a short summary — "12 s, 9:16, captions timed to the music; drag them if one feels early. Export costs $X." — and offer one next step: a 4:5 feed version, or a version without text for Stories.

## Variations

- **Only the user's photos, no AI**: 8–15 photos, 1–2 s each, `zoom_in` and `zoom_out` alternating, cuts on the beat, one transition style. Nothing to pay except the music (if new) and the export.
- **A trend format** ("POV: …", "A day in my life", "3 things…"): the hook text is the format itself; keep shots at 1–1.5 s.
- **The user talking to camera**: cut their clip into its best parts — the same source several times, each with its own `trim_start` and `duration` — to drop pauses and mistakes; captions for every phrase; music under it at 0.15.
