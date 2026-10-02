# Pacing and cuts

Editing is rhythm. The same shots feel dull or exciting depending only on how long each one stays on screen and where the cuts fall.

## How long each shot stays

| Energy | Seconds per shot |
| --- | --- |
| Hype, sport, music drops | 0.4–1.2 |
| Upbeat social video | 1–2.5 |
| Normal story or demo | 2–4 |
| Calm, luxury, emotional | 3–6 |
| Photos in a slideshow | 2.5–4 (with a slow zoom) |

- **Vary it.** Ten shots of exactly 2 seconds feel mechanical. Speed up toward the climax, hold a beat right before it, hit it, then let the ending breathe.
- **Open fast.** The first 3 seconds should be the quickest part of a social video.
- **Give the important shot more time** than the shots around it.

## Making cuts feel smooth

1. **Cut on movement.** End a clip while something is still moving and start the next one already in motion. A cut in the middle of movement hides itself; a cut on stillness shows.
2. **Keep the direction.** If the camera or subject moves left-to-right at the end of one shot, the next shot keeps moving left-to-right. A push-in hands over to a shot that starts close and keeps settling in. Plan these moves in the shot list — it's the biggest difference between "AI clips glued together" and an edit that flows.
3. **Match shapes and colours.** A round coffee cup → a round full moon; a red scarf → a red car. Match cuts feel clever without any effect.
4. **Use the trim.** With `trim_start` and `duration`, pick the exact seconds of each clip — usually the middle, where the motion is strongest and nothing has drifted yet.
5. **A hard cut is the default.** Most cuts need no transition at all. See [transitions](transitions.md) for when one helps.

## Cutting to music

- One beat lasts 60 ÷ BPM seconds. At 120 BPM a beat is 0.5 s, so a cut every 2 beats falls every 1.0 s and every 4 beats every 2.0 s.
- Rhythmic, energetic music: cut every 1, 2 or 4 beats, and put the strongest shot, title or logo on the big hit or drop.
- Calm music without a clear beat: change shots every 4–6 seconds on the musical phrases, with slow zooms and soft transitions — never fast cuts.
- You can't hear the track. When you made the music, time the cuts from the tempo you asked for and tell the user they're approximate — they can drag them into place in the editor. When the user brings a song, ask for its BPM or roughly where the drop is, or keep the cuts on a steady 2-second grid.
- A readable line of text needs at least one full beat on screen; anything shorter is just flicker.

## Timing the edit

Clips play one after another, so the video is as long as all clip durations added up (a transition happens across the cut and doesn't shorten the video). A text's `start` is its time on the final video — add up the durations of the clips before it.

Example — 120 BPM, cuts on 2 and 4 beats: clips of 1, 1, 2, 2, 3 and 3 seconds start at 0, 1, 2, 4, 6 and 9 s. A title on the last shot starts at 9.1 s.

## Stillness is a choice

A held, still shot is better than motion for its own sake. Don't add zooms, wobbles or loops just to "keep it alive". Every movement should mean something.
