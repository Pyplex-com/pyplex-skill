# Motion graphics

Title cards, ads, lower thirds, logo reveals, stats, announcements and end screens — made with `create_motion_design` and finished in Pyplex Motion Design. Making one is free; exporting costs the small fee shown in the result.

## Templates first

| Template | What it is | Shape, length | Values |
| --- | --- | --- | --- |
| `ad-card` | Headline and subheadline ad | 16:9, 6 s | headline, subheadline, brand-color |
| `app-ui-demo` | An animated app window with a headline | 16:9, 8 s | headline, brand-color |
| `lower-third` | Name and title bar for interviews | 16:9, 4 s | name, title, brand-color |
| `product-shot` | A product frame with a badge and a headline | 16:9, 7 s | headline, badge, brand-color |
| `social-hook` | A vertical opener for short videos | 9:16, 5 s | hook, subhook, brand-color |
| `kinetic-title` | Three words animating in | 16:9, 5 s | word-1, word-2, word-3, brand-color |
| `logo-reveal` | A brand name reveal | 16:9, 5 s | brand-name, brand-color |
| `end-screen` | A closing card with a call to action | 16:9, 6 s | headline, cta, brand-color |

- Fill the values with **short** words: a headline of 2–6 words, one line under it.
- The brand colour as a hex code from the user's brand.
- A template keeps its own shape. For another shape, build it with layers.
- You can add layers on top of a template — a logo, a photo, a sticker.

```json
{ "title": "Lower third — Riya", "template": "lower-third",
  "template_values": { "name": "Riya Sharma", "title": "Founder, Little Leaf Tea", "brand-color": "#19A877" } }
```

## Building with layers

Think of the frame as 1 × 1: `x` 0 is the left edge and 1 the right, `y` 0 the top and 1 the bottom, measured at each layer's centre; `width` and `height` are fractions of the frame. The first layer is at the back.

A clean stack, from back to front:

1. **Background**: the `background` colour, or a full-frame photo or video layer (`width` 1, `height` 1). Dim a photo with `opacity` 0.4–0.6 or a dark shape over it, so text on top stays readable.
2. **Shapes**: a bar, card or pill (`shape` "rectangle" with a `radius`, or "ellipse").
3. **The product or photo.**
4. **Text**: the headline (`size` "huge" or "large", `weight` "black" or "bold"), then the supporting lines ("medium", "regular").

## Timing: reveal in order

- Nothing appears all at once. Bring things in one after another, 0.2–0.4 s apart (`start`), in reading order: headline, then the line under it, then the button.
- Things arrive **when they matter** — with a voice-over, at the moment the voice says them.
- End with a calm hold: the finished layout sits still for the last 1–1.5 s so it can be read.
- Use an exit (`fade-out`) only when something must leave before the end.

## Entrances

| Feel | `enter` |
| --- | --- |
| Clean and modern — the default | `fade-in`, `slide-up-in` |
| Directional, "next" | `slide-left-in` |
| A card or panel turning over | `flip-in-3d` |
| A badge, sticker or button that should pop | `scale-pop` (a slight overshoot — once per design) |
| Playful | `rotate-in` |

## Loops — almost never

A loop keeps moving the whole time. Loop at most one thing: `pulse` on a call-to-action button (its shape and its text), or `float-loop` on a product photo. Never loop headlines or paragraphs — moving words are hard to read, and things bobbing for no reason look cheap. A still, finished layout beats one that wobbles.

## Layout

- 16:9: keep text between x 0.08 and 0.92, y 0.1 and 0.9.
- 9:16 for phones: keep everything important between y 0.12 and 0.78 and away from the right edge, where the apps put their buttons.
- Headlines up to about six words, `max_width` 0.7–0.85 so the lines wrap well.
- Two or three colours plus white. Text over a photo needs a dark shape or a dimmed photo behind it.
- Align things: centre everything, or give a left-aligned stack the same `x` and `align` "left".

## Real motion: keyframes, lines, counters, camera, sound

Entrances and exits cover most designs. When the idea needs something to **travel**, **draw**, **count** or the view to **move**, use these. A design can have up to 120 layers.

- **`keyframes`** on any layer: a list of moments, each with a `time` in seconds from the layer's own start and the values it reaches then — `x`, `y` (fractions of the frame), `scale` (1 = normal), `rotation` (degrees), `opacity` (0–1). `easing` says how it moves *into* that key: `ease-in-out` (default, calm), `ease-out` (fast then settles — for arrivals), `ease-in` (for leaving), `smooth`, `snappy` (quick, punchy), `linear` (steady — for scrolling or rotating), `hold` (jumps). Give the first key at `time` 0 with the starting values. Your keyframes replace the entrance/exit for the same value, so for a moving layer use `enter` "none" or animate a different value.
- **`path`** layer — a line or outline from `points` (`[x, y]` pairs, fractions of the frame): chart lines, arrows, underlines, routes on a map, a circle drawn around something. `stroke` colour, `stroke_width` in pixels, `closed` true with a `fill` for a filled shape. `draw` makes the line draw itself: `{ "start": 0.4, "duration": 1.2 }`.
- **`count`** on a text layer — a number that counts: `{ "from": 0, "to": 12500, "duration": 1.5, "suffix": "+ users" }`. Also `prefix` ("$", "₹"), `decimals`, `start`. Put the final value in `text` too.
- **`camera`** — moves the whole view: a list of `{ time, x, y, zoom }` from the design's start. `x`/`y` is the point at the centre of the screen, `zoom` 1 shows the whole frame, 2 is twice as close. A slow push-in (zoom 1 → 1.08 over the whole design) adds life to a still layout; a pan from one side of a wide layout to the other walks through steps. One camera move at a time, never fast.
- **`audio`** — music or sound effects: `{ "source": "generation:<id>", "start": 0, "volume": 0.8, "fade_out": 1 }`, up to 5. Make the music first (see [sound](sound.md)), then line the reveals up with its beats.

Keep it restrained: one hero motion per moment, everything else still. A counter, a drawing line and a camera move all at once is noise.

A growth stat with a counting number and a chart line that draws itself:

```json
{
  "title": "12,500 users",
  "aspect_ratio": "9:16",
  "duration": 6,
  "background": "#0B0F19",
  "layers": [
    { "type": "text", "text": "12,500+", "size": "huge", "weight": "black", "color": "#FFFFFF", "y": 0.3, "enter": "fade-in",
      "count": { "from": 0, "to": 12500, "duration": 1.8, "suffix": "+" } },
    { "type": "text", "text": "people joined this year", "size": "medium", "weight": "regular", "color": "#AAB4C8", "y": 0.38, "start": 0.6, "enter": "slide-up-in" },
    { "type": "path", "points": [[0.12, 0.72], [0.3, 0.66], [0.48, 0.68], [0.66, 0.56], [0.88, 0.46]], "stroke": "#19A877", "stroke_width": 10,
      "start": 0.8, "enter": "none", "draw": { "start": 0, "duration": 1.6 } },
    { "type": "shape", "shape": "ellipse", "x": 0.88, "y": 0.46, "width": 0.04, "height": 0.0225, "color": "#19A877", "start": 2.4, "enter": "scale-pop" }
  ],
  "camera": [{ "time": 0, "zoom": 1 }, { "time": 6, "zoom": 1.06, "easing": "linear" }],
  "audio": [{ "source": "generation:<music-id>", "volume": 0.7, "fade_out": 1 }]
}
```

A badge that flies in along a path of keyframes and settles:

```json
{ "title": "New badge", "duration": 4, "layers": [
{ "type": "text", "text": "NEW", "size": "medium", "weight": "black", "background": "#FF5A1F", "enter": "none",
  "keyframes": [
    { "time": 0, "x": 1.2, "y": 0.2, "rotation": 20, "opacity": 0 },
    { "time": 0.6, "x": 0.78, "y": 0.24, "rotation": -6, "opacity": 1, "easing": "ease-out" },
    { "time": 0.9, "rotation": 0, "easing": "smooth" }
  ] }
] }
```

## Inside a video

When the graphic belongs in a video you are editing, put it in `create_video_edit`'s `motion` list instead of making a separate design — the user gets one project with the clips, music and graphics together, and nothing to stitch by hand.

- Each item: `start` (seconds on the final video) and `design` — exactly what `create_motion_design` takes (layers, keyframes, path, count, camera, template), minus `aspect_ratio` (it takes the video's shape) and `audio` (music goes in the edit's `audio`).
- **No `background`** = the design floats over the video: lower thirds, stickers, counters, captions with motion, a chart over a shot.
- **A `background` colour** = it covers the screen for its `duration`: title cards, chapter cards, end screens. Time the clips so the story pauses there, or let the card sit over a clip you don't need to see.
- Templates work when their shape matches the video (`social-hook` for 9:16; the rest for 16:9).
- One design at a time (they can't overlap). Things that appear together — a headline and its number — go in one design.

A Reel with a counting stat over the first shot and an end card:

```json
{
  "title": "Café Reel",
  "aspect_ratio": "9:16",
  "clips": [
    { "source": "generation:<clip-1>", "duration": 4, "volume": 0, "transition": { "type": "zoomBlur", "duration": 0.3 } },
    { "source": "generation:<clip-2>", "duration": 4, "volume": 0 }
  ],
  "audio": [{ "source": "generation:<music-id>", "volume": 0.7, "fade_out": 1 }],
  "motion": [
    { "start": 0.5, "design": { "duration": 3, "layers": [
      { "type": "text", "text": "1,200+", "size": "huge", "weight": "black", "y": 0.18,
        "count": { "from": 0, "to": 1200, "duration": 1.2, "suffix": "+" } },
      { "type": "text", "text": "cups a week", "size": "medium", "y": 0.25, "start": 0.4, "enter": "slide-up-in" }
    ] } },
    { "start": 6, "design": { "duration": 2, "background": "#19A877", "layers": [
      { "type": "text", "text": "PYPLEX Café", "size": "huge", "weight": "black", "y": 0.45, "enter": "scale-pop" },
      { "type": "text", "text": "Open daily · 8 am", "size": "medium", "weight": "regular", "y": 0.56, "start": 0.3, "enter": "fade-in" }
    ] } }
  ]
}
```

## Examples

A stat card for a Reel:

```json
{
  "title": "2x faster checkout",
  "aspect_ratio": "9:16",
  "duration": 5,
  "background": "#0B0F19",
  "layers": [
    { "type": "shape", "shape": "rectangle", "x": 0.5, "y": 0.45, "width": 0.84, "height": 0.34, "color": "#151C2E", "radius": 48, "enter": "fade-in" },
    { "type": "text", "text": "2×", "size": "huge", "weight": "black", "color": "#FFD400", "y": 0.4, "start": 0.3, "enter": "scale-pop" },
    { "type": "text", "text": "faster checkout", "size": "large", "y": 0.52, "start": 0.7, "enter": "slide-up-in" },
    { "type": "text", "text": "Little Leaf Pay", "size": "small", "weight": "regular", "color": "#AAB4C8", "y": 0.7, "start": 1.2, "enter": "fade-in" }
  ]
}
```

An announcement over the user's photo, with one pulsing button:

```json
{
  "title": "Monsoon menu",
  "aspect_ratio": "16:9",
  "duration": 6,
  "layers": [
    { "type": "image", "source": "generation:<photo-id>", "width": 1, "height": 1, "opacity": 0.6, "enter": "fade-in" },
    { "type": "shape", "x": 0.5, "y": 0.5, "width": 1, "height": 1, "color": "#000000", "opacity": 0.35, "enter": "none" },
    { "type": "text", "text": "The monsoon menu is here", "size": "huge", "weight": "black", "max_width": 0.75, "y": 0.42, "start": 0.4, "enter": "slide-up-in" },
    { "type": "text", "text": "8 new dishes · from Friday", "size": "medium", "weight": "regular", "y": 0.6, "start": 0.9, "enter": "fade-in" },
    { "type": "shape", "x": 0.5, "y": 0.75, "width": 0.22, "height": 0.09, "color": "#FF5A1F", "radius": 999, "start": 1.4, "enter": "scale-pop", "loop": "pulse" },
    { "type": "text", "text": "Book a table", "size": "small", "y": 0.75, "start": 1.4, "enter": "scale-pop", "loop": "pulse" }
  ]
}
```
