# Writing prompts for Pyplex models

You write the prompt; the user describes what they want in their own words (any language). Write prompts in English unless the model or the user's text needs another language (for example lettering or speech in Hindi).

For whole videos — shots, camera moves, keeping a person the same in every shot — also read [shots](craft/shots.md) and [look](craft/look.md).

## Photo edits (keep the person)

Say **what changes** and **what must stay the same**.

- Change: "Add a glossy red sports car parked right behind the person, on the same street."
- Keep: "Keep the person's face, hair, pose, clothing and the camera angle exactly the same."
- Match: "Match the existing light and shadows; photorealistic."

One clear change per edit gives the most reliable result. For several changes, chain edits (`generation:<id>`).

## Several reference images

The top edit models take several images at once: `bytedance/seedream-v5.0-pro/edit` up to 10, `google/nano-banana-pro/edit` and `google/nano-banana-2/edit` up to 14, `openai/gpt-image-2.5-sunburst/edit` and `openai/gpt-image-2.5-flare/edit` up to 16. Pass them as a list in `files` — for example {"images": ["upload:<upload_id>:1", "upload:<upload_id>:2", "generation:<id>"]} — and refer to them by their order in the prompt:

> The woman from image 1 holds the perfume bottle from image 2 in the sunlit kitchen from image 3. Keep her face and the bottle's label exactly the same.

## New images from text

Subject → setting → light → camera → style. Example: "A street-food vendor making chai at dusk in an old Jaipur lane, warm string lights, steam rising, shallow depth of field, 35mm photo, natural colours."

For readable text in the image, put the exact words in quotes: `a poster with the headline "MONSOON SALE"`.

## Image → video

Describe **motion**, not the picture (the model already sees the picture):

- The action, in order: "He walks to the car, opens the driver's door and sits inside."
- The camera: "slow push-in", "static tripod shot", "smooth orbit to the left".
- Keep it physically simple: one main action per clip.
- Say what must not change: "keep his face and outfit consistent".
- The clip takes the frame shape of the start image. An end frame (`last_image`) decides where the shot lands.

## Text → video

Scene + action + camera + mood, like a short shot description: "Low-angle shot of a red sports car driving along a coastal road at sunset, camera tracking alongside, cinematic, warm light." With `bytedance/seedance-2.5/text-to-video` you can add `reference_images` (a person or product to keep), `reference_videos` (motion or camera to follow) and `reference_audios`.

## Music

Genre, mood, tempo, instruments and structure: "Upbeat Bollywood-pop instrumental, 120 BPM, dhol and synth bass, bright and festive, 30 seconds, clear ending." Add lyrics only if the model has a lyrics field. More in [sound](craft/sound.md).

## Speech

Give the exact words to say, plus how to say them if the model supports it (calm, excited, narrator). Check `get_model` for voice and language options.

## Avoid

- Real people's names to imitate them, and anything Pyplex's rules forbid (`read_docs` page `rules`).
- Brand logos the user doesn't own.
- Very long prompts with many conflicting ideas — clarity beats length.
