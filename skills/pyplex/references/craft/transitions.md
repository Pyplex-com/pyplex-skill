# Transitions

A transition says "something changed": a new place, a jump in time, a reveal. Most cuts in a good edit have **no** transition — a clean cut is the default. Save effects for the moments that deserve them.

In `create_video_edit`, a clip's `transition` is the effect from that clip into the next one.

## Rules

- **Pick one or two styles for the whole video** and repeat them. A different effect on every cut looks like a demo of effects.
- **Keep them short**: 0.2–0.4 s for energetic edits, 0.4–0.7 s normally, 0.8–1.5 s for slow, dreamy or emotional ones.
- **Match the motion.** A zoom transition works when the shot before it pushes in; a whip pan when the camera already moves sideways; a defocus when a shot ends soft.
- **Use the loud ones once or twice** (flashes, glitches, 3D) — the reveal, the drop, the logo.

## Which one

| Moment or mood | Transitions (`type`) |
| --- | --- |
| Calm, emotional, memories | `crossfade`, `lensDefocus`, `dreamyZoom`, `noiseDissolve` |
| Change of scene or time; the ending | `dipToBlack` (`dipToWhite` for bright, happy or dreamlike) |
| Energy, sport, beat drops | `zoomBlur`, `whipPan`, `linearBlur`, `zoom` |
| Modern, polished brand videos | `zoomBlur`, `lensDefocus`, `crossWarp`, `warpSwipe` |
| A reveal, or "before → after" | `doorway`, `cube`, `splitReveal`, `circleZoom`, `overexposure` |
| Flashback, memory, a burst of light | `overexposure`, `flash`, `filmBurn` |
| Tech, gaming, glitch looks | `rgbGlitch`, `glitch`, `pixelate`, `colorSplit` |
| Playful, kids, party | `swirl`, `spin`, `ripple`, `pageTurn`, `circleReveal` |
| Same scene, the next item in a list | a hard cut, `slide` or `push` |

The full list: crossfade, dipToBlack, dipToWhite, wipe, slide, zoom, push, circleReveal, blur, whipPan, radialWipe, pixelate, glitch, blinds, diamondReveal, spin, flip, splitReveal, flash, filmBurn, mosaic, ripple, pageTurn, colorSplit, zoomBlur, dreamyZoom, linearBlur, lensDefocus, warpSwipe, crossWarp, cube, doorway, swirl, morph, overexposure, rgbGlitch, noiseDissolve, windowSlice, circleZoom.

The last fifteen, from zoomBlur on, are GPU effects. On a device that can't run them, the editor plays a similar simpler effect and tells the user.

## Recipes

- **Smooth premium** (products, brands): hard cuts on the beat, `zoomBlur` for 0.3 s into the hero shot, `dipToBlack` for 0.8 s before the end card.
- **Dreamy** (weddings, memories): `crossfade` for 0.8–1.2 s throughout, and `overexposure` for 0.6 s once, at the big moment.
- **Hype** (sport, gaming, drops): hard cuts on every beat, `whipPan` for 0.25 s on changes of direction, `rgbGlitch` for 0.3 s on the drop.
- **Travel montage**: `whipPan` between places, `lensDefocus` for 0.5 s into the slow scenic shots.
