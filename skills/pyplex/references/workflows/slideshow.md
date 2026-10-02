# Photo slideshow: birthday, wedding, trip, memories

The user's own photos and clips, put together with music and a few words. Often it needs no AI generation at all — making the edit is free and only the export (and new music, if any) costs money.

Read first: [pacing](../craft/pacing.md), [text](../craft/text.md).

## 1. Collect

`request_upload_link` with kind "any" and up to 10 files ("Add up to 10 photos"); for more, a second link. Ask about the occasion, the names, any date or line they want on screen, and the mood (happy, emotional, funny).

## 2. Order it like a story

- In time order for trips and growing-up videos — or by feeling: start warm, build to the happiest moments, end on the best photo.
- Open with a strong photo (faces, smiles), not whichever came first.
- Group by place or moment, and change the pace between groups.
- Leave out near-duplicates; keep the best of each burst.

You usually can't see what's in the uploaded photos. If you can't, keep the upload order and ask the user which photo should open the video and which should close it.

## 3. The edit

- 2.5–4 s per photo (faster for a party, slower for emotional ones), alternating `zoom_in` and `zoom_out`.
- Mixed photo shapes (portrait photos in a 16:9 video): `fit` "contain" with `background` "blur" — nothing gets cut off.
- Transitions: `crossfade` for 0.8 s for emotional videos, or hard cuts on the beat for a party; one `overexposure` or `dipToWhite` for the big moment.
- Music: their song (upload, kind "audio") or a new instrumental from `elevenlabs/music-v2.5`, 2 s longer than the slideshow, with a 2-second `fade_out`.
- Text: a title at the start ("Happy 30th, Riya"), places or dates as `small` labels, a closing line on the last photo — with `fade` or `rise`.

## 4. Optional AI touches — each with its own price and yes

- Bring one or two key photos to life with `bytedance/seedance-2.5/image-to-video` and a subtle movement.
- Sharpen a blurry old photo with `clarity-ai/crystal-upscaler`.
- An animated title card from `create_motion_design` (`kinetic-title` or `logo-reveal`); the user exports it and adds it at the start in the editor.
