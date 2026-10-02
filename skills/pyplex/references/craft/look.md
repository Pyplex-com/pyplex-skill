# Look and consistency

The quickest way to look amateur is shots that don't belong together: different faces, different light, different colours. Decide the look once and repeat it everywhere.

## Write a look line and reuse it

Before the first image, write one look line and paste it, word for word, into every image and video prompt:

> warm golden-hour light, soft film grain, muted earthy colours with mustard accents, shallow depth of field, 35mm lens

It names the light (soft daylight, golden hour, neon night, studio softbox), the colours (2–3 main colours and one accent), the lens and focus (wide, 35mm, 85mm portrait, macro, shallow focus) and the texture (clean digital, film grain, glossy commercial).

## The same person in every shot

1. Start from the user's own photo (upload link): clear, facing the camera, good light. Two or three photos from different angles help even more.
2. Make every keyframe with a top edit model and **the same reference photo(s)** each time: `bytedance/seedream-v5.0-pro/edit` or `google/nano-banana-pro/edit` — both take several images (person + product + place).
3. Repeat the same short description in every prompt — "the same woman from the reference photo: shoulder-length black hair, round glasses, mustard kurta" — and say "keep her face exactly the same".
4. Keep the outfit unless the story changes it.
5. Animate those keyframes with image-to-video. For a text-to-video shot, give the person's photos as `reference_images` to `bytedance/seedance-2.5/text-to-video` (up to 30).
6. Check the face after every step. If it drifts, redo that shot — don't build on it.

The same method works for a product (same reference angle, colour and label), a pet or a place.

## Frame shape

| Where it's posted | `aspect_ratio` |
| --- | --- |
| Reels, TikTok, Shorts, Stories | 9:16 |
| YouTube, websites, TV | 16:9 |
| Instagram and Facebook feed | 4:5 (or 1:1) |

Make every image and clip in the final shape from the start. A 16:9 clip in a 9:16 edit is either cropped (`fit` "cover") or shown whole with a blurred background behind it (`fit` "contain").

## Composition

- Leave room for the text: if the title goes at the top, frame the subject lower.
- Put the subject on a third of the frame, not dead centre — unless it's a symmetrical hero shot.
- One clear subject per shot. If the eye has to search the frame, it's too busy.

## Avoid the "made by AI" look

- Inflated prompt words — "8k, masterpiece, ultra-detailed, hyper-realistic, trending" — make everything glossy and plastic.
- Purple-blue neon gradients and glowing particles floating over everything.
- Perfect plastic skin: ask for "natural skin texture" on people.
- A different style in every shot.
- Fake text and logos inside images — unless you ask a text-capable model for exact words in quotes (see [prompting](../prompting.md)).
