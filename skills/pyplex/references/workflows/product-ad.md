# Product ad or promo

Make people want the product in 10–30 seconds — even when all the user has is a phone photo of it.

Read first: [story](../craft/story.md), [shots](../craft/shots.md), [look](../craft/look.md), [transitions](../craft/transitions.md).

## 1. Brief

What the product is and who it's for, the one reason to buy (the promise), the offer and call to action, the brand colour (hex) and logo if they have them, and where the ad runs (that sets the frame shape).

## 2. Story

Pick one shape: problem → fix for useful products, show → explain → show for food and crafts, a mood montage for fashion and luxury. Five to eight beats:

1. Hook — the product at its most striking: a macro, a splash, a reveal.
2. The promise — 3–6 words on screen.
3. Two or three proof shots — the product in use, its details, the result.
4. The offer and the call to action on the final shot.

## 3. Hero images from the user's photo

1. `request_upload_link` (kind "image", 1–5 files): clear photos of the product, plus the logo.
2. Make 4–6 scenes with `bytedance/seedream-v5.0-pro/edit` or `google/nano-banana-pro/edit`, always from the same product photo — for example:
   > Place this exact bottle on wet black stone with a soft rim light and water droplets, dark and moody macro product photography; keep the label, logo and shape exactly the same.
   Variety: a hero on a plain background in the brand colour; the product in use (hands, a table, a shelf); a detail macro; a lifestyle scene with a person.
3. Check the label and logo in every result — products must stay exact.

## 4. Motion

Animate three to five scenes with `bytedance/seedance-2.5/image-to-video`: a slow orbit, a slow push-in, a pour or splash, light sweeping across the surface. Product shots look premium when the camera moves slowly and the product itself barely moves.

## 5. The edit

- 9:16 or 4:5 for social media, 16:9 for YouTube and websites.
- Music: modern and confident, 100–124 BPM, cut every 2 or 4 beats. `zoomBlur` into the hero shot, hard cuts elsewhere, `dipToBlack` or `overexposure` into the final shot.
- Text: the promise (`large`), two or three short benefits (`medium`), and the offer and call to action at the end in the brand colour.
- The last shot: the hero image with `motion` "zoom_in" for 3 s, holding the call to action. For an animated logo, make it separately with `create_motion_design` (`logo-reveal` or `end-screen`) — the user exports it and adds it at the end in the editor.

## Ad rules

- Show the product within the first two seconds.
- Benefits, not features: "Stays cold for 24 hours", not "double-wall steel".
- One offer, one call to action.
- Never invent claims ("No. 1 in India", "doctor approved"), prices or reviews — use only what the user tells you.
- No other brands' logos or products, and no celebrities.
