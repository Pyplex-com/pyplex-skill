# Choosing a Pyplex model

Pyplex has 900+ models and adds new ones often. This page lists **good starting points** by task. Always confirm with `search_models` (current list, starting prices) and `get_model` (exact settings) — model ids below were checked when this skill was released, and newer ones may be better.

## Pyplex's top picks — start here

These give the best results today. Use them unless the user names another model (`search_models` lists them first, marked `recommended`):

| Task | Top picks |
| --- | --- |
| Edit a photo (keep the person the same) | `bytedance/seedream-v5.0-pro/edit`, `google/nano-banana-pro/edit` (highest quality, costs more), `google/nano-banana-2/edit` (lower price), `openai/gpt-image-2.5-sunburst/edit` (fine detail, text), `openai/gpt-image-2.5-flare/edit` (fast) |
| New image from text | `bytedance/seedream-v5.0-pro`, `google/nano-banana-pro/text-to-image`, `google/nano-banana-2/text-to-image`, `openai/gpt-image-2.5-sunburst/text-to-image` (posters, readable text), `openai/gpt-image-2.5-flare/text-to-image` (fast) |
| Photo → video, text → video | `bytedance/seedance-2.5/image-to-video`, `bytedance/seedance-2.5/text-to-video` |
| Change or lengthen a video | `bytedance/seedance-2.5/video-edit`, `bytedance/seedance-2.5/video-extend` |

Match the **task** first, then quality vs. speed:

- Names ending in `-fast`, `-turbo`, `-flash`, `-lite` or `-std` are cheaper and quicker — good for drafts.
- `-pro`, `-max`, `-ultra`, `-4k` cost more — use when the user wants the best result or a final version.
- When unsure, quote two options and let the user choose.

## Images

| Task | Good starting points |
| --- | --- |
| Edit a photo, keep the person the same (add/remove things, new background, outfit, lighting) | `google/nano-banana-pro/edit`, `bytedance/seedream-v5.0-pro/edit`, `hosted/flux-2-pro/edit`, `openai/gpt-image-2/edit` |
| Combine several photos (person + product + place) | `google/nano-banana-pro/edit-multi`, `bytedance/seedream-v5.0-pro/edit` (takes several images) |
| New image from text | `google/nano-banana-pro/text-to-image`, `bytedance/seedream-v5.0-pro`, `hosted/flux-2-pro/text-to-image`, `openai/gpt-image-2/text-to-image` |
| Text, logos and posters (readable lettering) | `ideogram-ai/ideogram-v3-quality`, `openai/gpt-image-2/text-to-image` |
| Upscale / sharpen | `clarity-ai/crystal-upscaler`, `clarity-ai/creative-upscaler` (adds detail) |
| Remove the background | `bria/remove-background`, `hosted/image-background-remover` |

## Video

| Task | Good starting points |
| --- | --- |
| Animate a photo (image → video) | `kwaivgi/kling-v3.0-pro/image-to-video`, `google/veo3.1/image-to-video`, `bytedance/seedance-2.0/image-to-video`, `minimax/hailuo-2.3/i2v-pro`, `openai/sora-2/image-to-video` |
| Cheaper image → video drafts | `bytedance/seedance-2.5/image-to-video-turbo`, `google/veo3.1-fast/image-to-video`, `kwaivgi/kling-v3.0-std/image-to-video`, `minimax/hailuo-2.3/i2v-standard` |
| Video from text only | `google/veo3.1/text-to-video`, `kwaivgi/kling-v3.0-pro/text-to-video`, `bytedance/seedance-2.0/text-to-video`, `openai/sora-2/text-to-video`, `bytedance/seedance-2.5/text-to-video-turbo` (cheaper drafts) |
| Follow the motion or style of a reference video, keep a person from photos | `bytedance/seedance-2.5/text-to-video` (`reference_videos`, `reference_images`) |
| Make a clip longer | `google/veo3.1/video-extend`, `bytedance/seedance-2.0/video-extend` |
| Edit an existing video | `bytedance/seedance-2.0/video-edit` |
| Copy a movement onto a person | `kwaivgi/kling-v3.0-pro/motion-control` |
| Upscale a video | `clarity-ai/crystal-video-upscaler` |
| Remove a video's background | `hosted/video-background-remover` |

Video price depends on length and resolution — quote before promising anything. Start and end frames: Seedance 2.5 and Veo 3.1 take a `last_image`, Kling takes an `end_image`; check `get_model`.

## Audio

| Task | Good starting points |
| --- | --- |
| Speech / voice-over from text | `elevenlabs/eleven-v3`, `elevenlabs/multilingual-v2` (many languages), `elevenlabs/flash-v2.5` (fast) |
| Music from a description | `elevenlabs/music-v2.5`, `google/lyria-3-pro/music`, `hosted/ace-step-1.5` |
| Change or continue a song | `hosted/ace-step/audio-to-audio`, `hosted/ace-step/audio-outpaint` |
| Sound effects from a description | `mirelo-ai/sfx-1.6/text-to-audio`, `sonilo/v1/text-to-sfx` |
| Matching sound for a silent video | `hosted/mmaudio-v2`, `mirelo-ai/sfx-1.6/video-to-video`, `kwaivgi/kling-video-to-audio` |

Voice cloning models exist — only with the voice owner's permission (Pyplex rules).

## Reading `get_model`

- `required: true` fields must be filled. Fields with `kind: "media"` are files — pass them in `files`, never in `settings`.
- `select` fields: use one of `options` exactly. `slider`/`number`: stay within `min`/`max`.
- `multiple: true` media fields take a list (up to `max_items`).
- Leave optional settings out unless the user asked for them or they clearly help (for example `aspect_ratio: "9:16"` for a phone video, `resolution` for print).
