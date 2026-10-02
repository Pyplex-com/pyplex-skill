# A short story with the same character

A 20–60 second story — a funny moment, a love story, a day in someone's life, a fable for children — with the same character in every shot. It's told with pictures, music and narration or captions.

Read first: [story](../craft/story.md), [shots](../craft/shots.md), [look](../craft/look.md), [sound](../craft/sound.md).

## 1. Write it first

- A one-line premise, and the ending — know the payoff before anything else.
- The story shape: setup → something changes → it gets harder → the turn → payoff. Six to twelve shots.
- One short narration or caption line per beat — or no words at all, just music.

## 2. Build the character, and get a yes on the look

1. A character sheet: one full-body image of the character on a plain background, in the look you chose — `bytedance/seedream-v5.0-pro` or `google/nano-banana-pro/text-to-image`. Or start from the user's own photo.
2. Show it and adjust until the user likes it. This image is the reference for everything after it.
3. Write the character line you'll repeat in every prompt: "Mintu, a small orange cat with a white chest and a blue collar".

## 3. Keyframes, then motion

1. One keyframe per shot, made from the character sheet with an edit model: "the same cat from the reference, now sitting on a rainy windowsill at night, looking sad, wide shot" plus the look line.
2. Compare all the keyframes side by side before animating — fixing an image is far cheaper than fixing a video.
3. Animate each with `bytedance/seedance-2.5/image-to-video`: one simple action per shot.

## 4. Sound and words

- Narration: one voice file per part of the story ([sound](../craft/sound.md)), or captions only.
- Music that follows the story: soft at the setup, tension in the middle, release at the payoff. Put those changes, with their timings, in the music prompt.
- A few sound effects on key moments: a door, thunder, a meow.

## 5. Edit

Shots of 2–5 s (slower than a Reel), hard cuts or `crossfade`, `dipToBlack` for jumps in time, a title at the start or the end, and a caption for each line.

Cost: a ten-shot story means ten video generations. Show the total first and offer a shorter version of five or six shots.
