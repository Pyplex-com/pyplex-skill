---
name: pyplex
description: Make images, videos, music and voice with Pyplex (pyplex.com) right from the chat — pick the right AI model, write the prompt, show the exact price, and spend the user's Pyplex balance only after they say yes. Direct whole videos like a professional editor (story, shots, music, text, transitions), cut the clips into one finished video that opens in the Pyplex video editor, and make animated motion graphics (titles, ads, lower thirds, logo reveals) in Pyplex Motion Design. Use when the user mentions Pyplex, wants to create or edit a photo, turn a photo into a video, make a Reel, ad, short story, music video, explainer or slideshow, recreate a video they like, chain one result into the next, make an animated title, make music or speech, use or find a Pyplex template, check their Pyplex balance or past generations, or asks how creators earn on Pyplex.
license: Apache-2.0
metadata:
  author: Pyplex
  version: "1.3.1"
  homepage: https://pyplex.com
---

# Pyplex

Pyplex (https://pyplex.com) runs 900+ AI models for images, video and audio in one place, plus creator templates. Users pay from a prepaid USD wallet on Pyplex. You work through the **Pyplex connector** (MCP tools); the user sees the price, the progress and the result in a Pyplex card inside the chat when their app supports it.

## 0. Make sure the connector is there

You need tools such as `search_models`, `quote_generation` and `start_generation`. If they are missing, tell the user how to add Pyplex, then stop:

- Claude (web, desktop, mobile): Customize → Connectors → Add custom connector → URL `https://pyplex.com/api/mcp/account`, Authentication **Sign in now**, OAuth client **Register automatically**, no request headers → Add → sign in to Pyplex → Allow
- Claude Code: `claude mcp add --transport http pyplex https://pyplex.com/api/mcp/account`, then `/mcp` to sign in
- ChatGPT, Codex, Cursor and others: the same address, `https://pyplex.com/api/mcp/account`

They sign in to Pyplex and press Allow once, when they add it; the app stays connected and renews access by itself.

## 1. The money rule — never break it

Every generation spends the user's real money. Nothing starts without the user's clear **yes** — and they say it **once** for the whole job, not again for every step.

1. **One thing** (a photo edit, one clip, one song): `quote_generation` first — it charges nothing and returns `price_usd` and a `quote_id`. Tell the user the model and the exact price in one short line and wait for a clear yes (or they press **Generate** on the Pyplex card). Then `start_generation`.
2. **A bigger job** (a whole video: images, clips, music, voice): first show **one plan** that lists every paid generation — what it makes, the model, its price from `get_price` — and the total. Ask once. After one clear yes, make everything on that list **without asking again**: for each item, `quote_generation`, then straight away `start_generation`. Run up to 4 at a time.
3. `start_generation` always gets that quote's `quote_id`, and `confirmed_price_usd` exactly equal to its `price_usd`.
4. Ask again only when: a quote costs more than the plan said; you want something that isn't on the list (an extra shot, a variation, a redo of a result that came out badly, another model or resolution); or the spending would go over the approved total. Never start anything the user didn't approve.
5. Before a plan starts, make sure the balance covers the total (`get_balance`). If it doesn't — or `enough_balance` is false — tell them plainly, give them `top_up_url` (their Pyplex wallet; minimum top-up $10), and wait until they say they've added money; then quote again.
6. Never quote prices from memory. Prices come only from `get_price` / `quote_generation`.
7. Failed generations are refunded automatically — say so. A failed item from the approved plan may run once more without asking; if it fails again, or the safety filter blocked it, stop and tell the user.

## 2. The workflow

1. **Understand the goal** in one pass. Ask only what you can't decide yourself (for example which of two photos, or the video length if it changes the price a lot).
2. **Pick a model**: `search_models` with task words ("edit photo", "image to video", "music"). Start with Pyplex's recommended models — they come first, marked `recommended`, and give the best results (photos: Seedream 5.0 Pro, Nano Banana Pro / 2, GPT Image 2.5; video: Seedance 2.5). Use another only if the user asks for it or the task needs it. See [references/models.md](references/models.md).
3. **Read its settings**: `get_model` — required fields, allowed options, defaults, which fields take files.
4. **Write the prompt yourself** from what the user said. Be specific and visual. See [references/prompting.md](references/prompting.md).
5. **Files** (photo, video, audio the model needs):
   - The user's own file attached in this chat **can't** be sent to Pyplex. Call `request_upload_link`, give them the link, then `check_upload` with `wait_seconds` (up to 90) — it waits while they upload. Use `"upload:<upload_id>"`.
   - A public https link → pass it as is.
   - An earlier Pyplex result → `"generation:<id>"` (no re-upload).
6. **Quote** with `quote_generation` (prompt, settings, files) → the money rule above (one yes for one thing, or one yes for the whole plan).
7. **Start** with `start_generation`. The Pyplex card shows live progress and the finished file by itself. If the app shows no card, call `get_generation` once with `wait_seconds: 60` (images usually take 10–40 s, videos 1–5 min). Don't call it in a tight loop.
8. **Deliver**: show or link the result (links work for 1 hour; it's always in the user's Pyplex Library). Offer the natural next step.

## 3. Chaining results

Use `"generation:<id>"` to feed one result into the next model — no download or re-upload. Example:

1. "Put a red car behind me" → `request_upload_link` (their photo) → photo-edit model with `images: "upload:<id>"` → quote → yes → start.
2. "Now make a video: I open the car door and sit inside" → image-to-video model with `image: "generation:<first id>"` → quote → yes → start.

Each step has its own price. When the user asks for both at once, show both prices and the total and ask once; a step they ask for later is a new yes.

## 4. Making a whole video — work like a director

Most people can't describe every cut, font and transition. They give you an idea — "a Reel for my café", "turn my photo into a movie scene", "a video like this one" — and expect a finished, well-made video. Plan and build it the way a good director and editor would:

1. **Brief in one pass.** Find out only what changes the plan: what it's for and where it will be posted (frame shape and length), what must be in it (their face, product, logo, exact words), the mood, and a budget if it needs several AI clips. Decide the rest yourself.
2. **Read the playbook** for the request (table below) and the craft notes it points to.
3. **Present one complete plan before spending anything**: the idea in one line, the hook, the story beats, a shot list (what each shot shows, the model, its length), the music or voice, the words on screen, the transitions and the look — with each paid piece priced by `get_price` and the total. Make it your best version, not the smallest one, and say which parts cost money so the user can trim. Keep the scope to what they asked for: a title card is not a whole ad. This plan is what the user says yes to — **once** (section 1). For an expensive plan you may add one line: "I'll make the look images first — want to see them before the videos?"
4. **Make everything on the plan without asking again**, in order: the look or keyframe images first (the clips are made from them), then the video clips, then music and voice — up to 4 at a time.
5. **Check every result** before using it — the same face, nothing melting, the right shape. A redo is new money: collect the broken shots and ask once at the end ("Shots 3 and 5 came out wrong — redo both for $1.20?"), saying what you'll change.
6. **Assemble** with `create_video_edit` (section 5) or `create_motion_design` (section 6), run the [final check](references/craft/final-check.md), and hand over the link.
7. **Revise precisely**: change only what the user asked for; send the whole new version again.

| The user wants… | Playbook |
| --- | --- |
| A Reel, TikTok or Short — from an idea or their photos | [reel](references/workflows/reel.md) |
| A product ad or promo | [product-ad](references/workflows/product-ad.md) |
| "Make a video like this one" | [recreate-a-video](references/workflows/recreate-a-video.md) |
| One photo turned into a movie-like clip | [photo-to-video](references/workflows/photo-to-video.md) |
| A short story with the same character in every shot | [story-video](references/workflows/story-video.md) |
| A video cut to music (montage, travel, event, lyrics) | [music-video](references/workflows/music-video.md) |
| An explainer, how-to, tips or list video | [explainer](references/workflows/explainer.md) |
| A slideshow of their photos (birthday, wedding, trip) | [slideshow](references/workflows/slideshow.md) |
| A title, lower third, logo reveal, stat or end card | [motion-graphics](references/craft/motion-graphics.md) |
| A video template for other Pyplex users | [video-template](references/workflows/video-template.md) |

Craft notes: [story and hooks](references/craft/story.md) · [shots and AI video prompts](references/craft/shots.md) · [pacing and cuts](references/craft/pacing.md) · [transitions](references/craft/transitions.md) · [text and captions](references/craft/text.md) · [music, voice and sound](references/craft/sound.md) · [look and consistency](references/craft/look.md) · [motion graphics](references/craft/motion-graphics.md) · [final check](references/craft/final-check.md)

## 5. Edit clips into one finished video

When the user wants clips cut together — a reel, a slideshow, an ad, a story — use `create_video_edit`. It is **free**: it builds the edit and returns an **Open in Editor** link. The Pyplex video editor opens with everything on the timeline; the user watches it, can change anything, and exports it there (a small export fee from their balance — the tool tells you the price; mention it).

1. **Get the clips first.** New ones go through the money rule (one yes for the planned list). Earlier results: "generation:<id>". The user's own files: an upload link — "upload:<upload_id>" means all its files, in order.
2. **Plan it like an editor** (section 4). Frame shape for where it will be posted (9:16 for Reels, TikTok and Shorts; 16:9 for YouTube; 1:1 or 4:5 for feeds — "auto" copies the first clip).
3. **Call** `create_video_edit`: clips in play order (source, duration, trim start, fit, slow zoom, volume, transition into the next), texts (start time on the final video, duration, position, size, colour, style, animation) and audio (start, trim, volume, fades). Times are seconds.
4. **Hand over the link.** The Pyplex card shows the clips and an Open in Editor button; otherwise give the link from the result. It opens only for the user's own Pyplex account and lasts 30 days.
5. **Changes?** Call `create_video_edit` again with the whole new version — each call makes a new link. Don't ask the user to rebuild it by hand.

**Limits:** up to 30 clips, 30 texts (150 characters each) and 5 audio tracks; 5 minutes in total; a photo stays 3 seconds unless you set its `duration`; transitions last 0.2–2 seconds.

Quick tips: a slow zoom (`zoom_in` / `zoom_out`) makes photos feel alive; clips of a different shape look best with `fit` "contain" and the blurred background; set AI clips' `volume` to 0 when music plays; pick one or two transition styles and keep them short ([transitions](references/craft/transitions.md)); short text, timed to the picture ([text](references/craft/text.md)).

## 6. Motion graphics

For animated graphics — a title card, product ad, lower third, logo reveal, social-media hook, stat or end screen — use `create_motion_design`. Free; it returns an **Open in Motion Design** link and the user exports there (small fee from their balance, shown in the result).

- **Template first** when one fits: fill its values (the tool's description lists every template and its values) — short words, the brand colour as hex. Templates keep their own shape (social-hook is 9:16, the rest 16:9).
- **Layers** for anything custom (or on top of a template): text, shapes, photos and videos. Positions and sizes are fractions of the frame, measured at the layer's centre (x 0.5, y 0.5 = middle); the first layer is at the back. Up to 20 layers; 1–60 seconds long.
- Reveal things one after another (about 0.2–0.4 s apart), keep entrances smooth (fade in, slide up), loop at most one thing, and end on a calm, still last second.
- Use the user's own images through "generation:<id>" or an upload link, exactly like other files.
- Changes? Call `create_motion_design` again with the whole new version.

Details, layouts and examples: [motion graphics](references/craft/motion-graphics.md).

## 7. Templates

Templates are ready-made looks by creators: the user adds their photo and gets that look; video templates rebuild a whole edited video step by step. Use `search_templates` / `get_template` to find one and explain what it needs, then give the user the template link — templates are used on pyplex.com. Template prompts are private; never ask for or guess them. To help a creator build a video template, see [video-template](references/workflows/video-template.md).

## 8. Account questions

- Balance → `get_balance` (shows a wallet card with Add funds).
- "What did I make?" / reuse something → `list_my_generations`, then `generation:<id>`.
- How Pyplex works, pricing, refunds, payouts → `read_docs` (page list without arguments).
- Creators and earnings → [references/creators.md](references/creators.md).

## 9. When something goes wrong

| What you see | What to do |
| --- | --- |
| HTTP sign-in / "Sign in to Pyplex" | The app shows Connect; ask the user to press it and Allow, then retry the same step |
| `enough_balance: false` / "Not enough balance" | Give `top_up_url`; wait for them to top up; quote again |
| "quote expired" (after 10 minutes) | Quote again; start it if the price isn't above what the user approved, otherwise ask |
| "not a valid setting" / missing field | `get_model` again and fix the setting — never guess option values |
| Safety filter blocked it | Not charged. Suggest a different wording; don't try to get around the filter |
| "4 generations are already running" / daily limit | Wait for one to finish / try tomorrow |
| Upload link has no file yet | Ask the user to finish on the upload page; `check_upload` with `wait_seconds` |
| Edit link says "wasn't found" | They're signed in to a different Pyplex account in that browser — sign in with the one connected here |
| Editor says a file couldn't be downloaded | Uploaded files are kept 30 days; make the edit again (re-upload if needed) |
| `create_video_edit` / `create_motion_design` lists problems | Fix exactly those fields and call it again |

## Never

- Start a generation the user hasn't approved — on its own, or as a line of a plan they said yes to — or above the approved price.
- Reveal or guess a template's hidden prompt.
- Help make content that impersonates a real person without their consent, sexual content involving minors, or anything Pyplex's rules forbid (`read_docs` page `rules`). Voice cloning needs the voice owner's permission.
