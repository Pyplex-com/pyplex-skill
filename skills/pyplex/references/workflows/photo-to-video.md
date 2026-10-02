# One photo → a movie-like clip

The user has one photo — a portrait, a product, a landscape, an old family picture — and wants it to move, or to become a short scene.

Read first: [shots](../craft/shots.md).

## The simple version: one clip

1. The photo: `request_upload_link` → `check_upload`.
2. The model: `bytedance/seedance-2.5/image-to-video` (5 s and 720p by default; 1080p for a final).
3. Describe only the motion and the camera — the picture is already there:
   - Portrait: "She slowly turns toward the camera and smiles, her hair moving in a light breeze, slow push-in, keep her face exactly the same."
   - Landscape: "Clouds drift, the water ripples, birds cross the sky, slow aerial push forward."
   - Product: "Slow orbit around the watch, light sweeps across the glass, the watch stays still."
   - Old photo: "Gentle natural movement: they blink and smile, slight head turns, static camera, keep the photo's colours." Mention that the movement is imagined by AI, not a real memory.
4. Quote → yes → start → show it.

## The scene version: 2–4 shots

To turn the photo into a little film:

1. Plan three shots that tell one moment: wide (where), medium (the action), close (the feeling).
2. Make the other keyframes from the original photo with an edit model: "the same man, now seen from behind, walking toward the sea; same clothes, same light".
3. Animate each one, using `last_image` where you want to control how a shot ends.
4. Edit: 9:16 or 16:9, cuts on movement, `lensDefocus` or `crossfade` between shots, soft music, a title if they want one.

## Making it longer

`bytedance/seedance-2.5/video-extend` continues a clip ("he keeps walking toward the water as the camera rises"). Making the next shot from a new keyframe usually looks better than extending again and again.

## Common requests

| They say | You do |
| --- | --- |
| "Put me in this place" / "with this car" | Edit the photo first (`bytedance/seedream-v5.0-pro/edit`), then animate the result with "generation:<id>" |
| "Make it cinematic" | 16:9, a slow push-in, shallow depth of field, a warm colour grade, soft music and a `dipToBlack` ending |
| "Make it longer" | A second shot from a new keyframe, then cut the two together |
