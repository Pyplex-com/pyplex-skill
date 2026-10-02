# Shots: directing the AI camera

Think in **shots**, not in "a video". One AI clip = one shot = one subject, one action, one camera move. Several short shots cut together look far better than one long generation asked to do everything.

## Shot sizes and what they say

| Shot | Shows | Use it for |
| --- | --- | --- |
| Wide / establishing | The whole place | Where we are; openings; scale |
| Medium | A person from the waist up, a product on a table | What is happening |
| Close-up | A face, hands, the product | Emotion, detail, the hero moment |
| Extreme close-up / macro | Texture: steam, drops, fabric, sparks | Quality, appetite, luxury |
| Top-down | Straight down at a table or desk | Food, flat lays, steps of a process |
| POV / over-the-shoulder | What the person sees | Putting the viewer inside the action |
| Low angle | Looking up | Power, heroes, cars, buildings |
| High angle | Looking down | Smallness, loneliness, an overview |

Mix sizes: wide → medium → close keeps the eye interested. Two almost identical framings back to back look like a mistake.

## Camera moves video models understand

| Move | Feels like | Good for |
| --- | --- | --- |
| Static (locked-off) | Calm, confident | Products, faces, holding a moment |
| Slow push-in | "This matters" | Faces, reveals, emotional beats |
| Pull-back reveal | "There's more" | Showing the place or the scale at the end |
| Tracking / follow | Energy, a journey | Walking, running, cars |
| Orbit around the subject | Premium, 3D | Product hero shots, a person posing |
| Crane up / rise | A grand finish | Endings, skylines, crowds |
| Handheld | Real, documentary | Street scenes, behind the scenes |
| Drone or FPV fly-through | Wow, speed | Travel, property, big spaces |
| Whip pan | A burst of speed | The last moment of a shot, into the next |
| Rack focus | Attention shifts | Moving from one object to another |

One move per shot. "Orbit while zooming while panning" gives wobbly results.

## Writing a video prompt

`[shot size and angle] of [subject and how they look], [one action, in order], [camera move], [place, light, time of day], [the look line], [what must stay the same]`

> Medium close-up of a young woman in a mustard kurta at a café window; she lifts her cup, smiles and looks outside; slow push-in; warm morning light through the glass; soft film look with gentle grain; keep her face and outfit exactly the same.

- **Image → video**: the picture is already there — describe only the motion and the camera. "Slowly" and "subtle" keep faces stable.
- **Text → video**: describe the scene as well, like one line of a film script.
- Put words for the screen in the edit, not in the video prompt — video models scramble letters.
- Avoid what AI video still does badly: hands doing fiddly work, several people touching, fast complicated physics, long single takes on a face. Keep those shots short or frame around them.

## Length, trimming and frame shape

- Seedance 2.5 clips are 4–30 seconds (5 by default). For a fast edit, make 4–5 seconds and keep the best 1.5–3 seconds with `trim_start` and `duration` in the edit. Skip the first half-second of an image-to-video clip — it starts on the still photo before the motion builds.
- The ends of AI clips are where things drift or melt. Cut before them.
- `bytedance/seedance-2.5/image-to-video` has no frame-shape setting: the clip takes the shape of its start image. Make the start images in the final shape first (`aspect_ratio` "9:16" on the image model for a Reel). Text-to-video has its own `aspect_ratio`.
- Draft cheap and fast (720p, the default, or `bytedance/seedance-2.5/image-to-video-turbo`); use 1080p for the final. Check prices with `get_price`.

## Start and end frames — the pro trick

`bytedance/seedance-2.5/image-to-video` takes a start `image` and an optional end frame, `last_image`. You decide where the shot begins **and** where it lands:

1. Make keyframe pictures first — cheap, and the user can approve the look before any video is paid for: K1, K2, K3, the same person or product in the same light.
2. Shot 1 goes K1 → K2, shot 2 goes K2 → K3. The cut between them disappears: shot 2 starts exactly where shot 1 ended, so separate clips play like one long, smooth camera move.
3. For a reveal: start on a close detail, end on the full product.

To continue a clip that ended too soon: `bytedance/seedance-2.5/video-extend`.

## Sound from the video model

`generate_audio` is on by default in Seedance — it adds matching ambient sound and effects. Keep it for realistic scenes. When music carries the video, set the clip's `volume` to 0 in the edit (and ask `get_price` whether turning `generate_audio` off costs less).

## Check every clip before you edit

Look at each result: is the face the same? Are the hands fine? Does anything melt at the end? Redo only the broken shot — with a new quote and a new yes — and say what you'll change ("her face changed in the last second; I'll make it 4 s with a slower push-in").

## Shot list format

| # | Place in the edit | Shot | Model and settings | Start → end image | Prompt (short) |
| --- | --- | --- | --- | --- | --- |
| 1 | 0.0–1.0 s | Macro: ice drops into cold coffee | Seedance 2.5 image-to-video, 4 s, 1080p | K1 | Ice cubes fall in slow motion, static camera |
| 2 | 1.0–2.0 s | Medium: barista slides the glass | Seedance 2.5 image-to-video, 4 s, 1080p | K2 → K3 | She slides the glass toward camera, slow push-in |
