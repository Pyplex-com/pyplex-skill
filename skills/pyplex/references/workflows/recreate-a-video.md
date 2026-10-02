# "Make a video like this one"

The user shows a video they like and wants the same kind of video with their own face, product or brand.

## 1. Understand the reference

Most chat apps can't play a video to you. Ask for whatever is easiest for them:

- 4–8 screenshots — the first frame, one from each different shot, the last frame — and roughly how long it is; or
- a short description: what happens, how fast it cuts, the text on screen, the music.

If your app can watch videos, watch it.

Then write down what makes it work — its recipe, not its content:

| What | Notes |
| --- | --- |
| Length and shape | 15 s, 9:16 |
| Hook | Opens mid-action on a close-up |
| Shots | 8 shots, about 2 s each; close → wide → close |
| Camera | Slow push-ins; one fast whip pan |
| Transitions | Hard cuts on the beat; one flash before the reveal |
| Text | 3–4 big words, centred, white with a yellow key line |
| Look | Warm golden hour, film grain |
| Music | Upbeat, about 120 BPM, the drop at 7 s |

Show this breakdown to the user in a few lines and check it's what they liked about it.

## 2. Rebuild it with their material

- **Their face**: their photos → one keyframe per shot with an edit model ([look](../craft/look.md): the same person in every shot) → `bytedance/seedance-2.5/image-to-video` with the reference's camera moves.
- **Borrow the reference's motion directly**: upload the clip (`request_upload_link`, kind "video") and give it to `bytedance/seedance-2.5/text-to-video` as `reference_videos`, with the user's photo in `reference_images`. Say what to take from it: "Follow the camera movement and pacing of the reference video; the person is the woman from the reference image; a rooftop at sunset." Trim the reference to the part that matters before uploading.
- **A dance or an exact body movement**: `kwaivgi/kling-v3.0-pro/motion-control` — the user's photo as `image`, the movement clip as `video`.
- **Music**: make a new track in the same style and tempo ([sound](../craft/sound.md)), never the original song. The user can add a track they own in the editor.
- **Text**: the same positions, sizes and rhythm — in their own words.

## 3. Edit to the same rhythm

Follow the breakdown: the same number of shots and lengths, transitions at the same moments, text at the same times ([pacing](../craft/pacing.md)). Then the [final check](../craft/final-check.md).

## Say the limits kindly

- Recreate the style, not the content: no copying someone's footage, music, logo or characters.
- Put a real person in a video only if it's the user themself or someone who agreed. No celebrities, and no one's face without their consent.
- A reference video the user uploads must be one they're allowed to use.
