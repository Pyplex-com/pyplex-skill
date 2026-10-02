---
name: pyplex
description: Make images, videos, music and voice with Pyplex (pyplex.com) right from the chat — pick the right AI model, write the prompt, show the exact price, and spend the user's Pyplex balance only after they say yes — edit several clips into one finished video (order, cuts, text, music, transitions) that opens in the Pyplex video editor, and make animated motion graphics (titles, ads, lower thirds, logo reveals) in Pyplex Motion Design. Use when the user mentions Pyplex, wants to create or edit a photo, turn a photo into a video, chain one result into the next, cut clips into a reel, slideshow or ad, make an animated title or motion graphic, make music or speech, use or find a Pyplex template, check their Pyplex balance or past generations, or asks how creators earn on Pyplex.
license: Apache-2.0
metadata:
  author: Pyplex
  version: "1.2.4"
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

Every generation spends the user's real money.

1. `quote_generation` first. It charges nothing and returns `price_usd` and a `quote_id`.
2. Tell the user the model and the exact price, in one short line. Wait for a clear **yes** (or they press **Generate** on the Pyplex card).
3. Only then call `start_generation` with that `quote_id` and `confirmed_price_usd` exactly equal to `price_usd`.
4. Get a fresh yes for **every** generation — retries, variations and "one more" included. Never start something they didn't ask for.
5. Never quote prices from memory. Prices come only from `get_price` / `quote_generation`.
6. If `enough_balance` is false (or `start_generation` says the balance is too low): tell them plainly, give them `top_up_url` (their Pyplex wallet; minimum top-up $10), and don't start until they say they've added money — then quote again.
7. Failed generations are refunded automatically. Say so if one fails.

## 2. The workflow

1. **Understand the goal** in one pass. Ask only what you can't decide yourself (for example which of two photos, or the video length if it changes the price a lot).
2. **Pick a model**: `search_models` with task words ("edit photo", "image to video", "music"). Start with Pyplex's recommended models — they come first, marked `recommended`, and give the best results (photos: Seedream 5.0 Pro, Nano Banana Pro / 2, GPT Image 2.5; video: Seedance 2.5). Use another only if the user asks for it or the task needs it. See [references/models.md](references/models.md).
3. **Read its settings**: `get_model` — required fields, allowed options, defaults, which fields take files.
4. **Write the prompt yourself** from what the user said. Be specific and visual. See [references/prompting.md](references/prompting.md).
5. **Files** (photo, video, audio the model needs):
   - The user's own file attached in this chat **can't** be sent to Pyplex. Call `request_upload_link`, give them the link, then `check_upload` with `wait_seconds` (up to 90) — it waits while they upload. Use `"upload:<upload_id>"`.
   - A public https link → pass it as is.
   - An earlier Pyplex result → `"generation:<id>"` (no re-upload).
6. **Quote** with `quote_generation` (prompt, settings, files) → the money rule above.
7. **Start** with `start_generation`. The Pyplex card shows live progress and the finished file by itself. If the app shows no card, call `get_generation` once with `wait_seconds: 60` (images usually take 10–40 s, videos 1–5 min). Don't call it in a tight loop.
8. **Deliver**: show or link the result (links work for 1 hour; it's always in the user's Pyplex Library). Offer the natural next step.

## 3. Chaining results

Use `"generation:<id>"` to feed one result into the next model — no download or re-upload. Example:

1. "Put a red car behind me" → `request_upload_link` (their photo) → photo-edit model with `images: "upload:<id>"` → quote → yes → start.
2. "Now make a video: I open the car door and sit inside" → image-to-video model with `image: "generation:<first id>"` → quote → yes → start.

Each step has its own price and its own yes.

## 4. Edit clips into one finished video

When the user wants clips cut together — a reel, a slideshow, an ad, a story — use `create_video_edit`. It is **free**: it builds the edit and returns an **Open in Editor** link. The Pyplex video editor opens with everything on the timeline; the user watches it, can change anything, and exports it there (a small export fee from their balance — the tool tells you the price; mention it).

1. **Get the clips first.** New ones go through the normal money rule (each needs its own yes). Earlier results: "generation:<id>". The user's own files: an upload link — "upload:<upload_id>" means all its files, in order.
2. **Plan it like an editor.** Frame shape for where it will be posted (9:16 for Reels, TikTok and Shorts; 16:9 for YouTube; 1:1 or 4:5 for feeds — "auto" copies the first clip). Photos 2–4 seconds each. Trim videos to the best part. Short, readable text — one line at a time, big enough to read on a phone. Music under everything, with a gentle fade out.
3. **Call** `create_video_edit`: clips in play order (source, duration, trim start, fit, slow zoom, transition into the next), texts (start time on the final video, position, size, colour, style, animation) and audio (start, volume, fades). Times are seconds.
4. **Hand over the link.** The Pyplex card shows the clips and an Open in Editor button; otherwise give the link from the result. It opens only for the user's own Pyplex account and lasts 30 days.
5. **Changes?** Call `create_video_edit` again with the whole new version — each call makes a new link. Don't ask the user to rebuild it by hand.

Tips: a slow zoom (zoom in or out) makes still photos feel alive. Clips of a different shape: fit "contain" with background "blur" shows all of the clip without black bars. AI videos often have no useful sound — set their volume to 0 when music plays. Transitions: crossfade for calm, dipToBlack between scenes; for a modern, polished look use zoomBlur or whipPan for energy, lensDefocus or noiseDissolve for soft cuts, cube or doorway for a 3D reveal, overexposure or rgbGlitch for punch. Pick one or two styles per video and keep them under a second. Total length up to 5 minutes.

## 5. Motion graphics

For animated graphics — a title card, product ad, lower third, logo reveal, social-media hook, end screen — use `create_motion_design`. Free; it returns an **Open in Motion Design** link and the user exports there (small fee from their balance, shown in the result).

- **Template first** when one fits: fill its values (the tool's description lists every template and its values) — short words, the brand colour as hex. Templates keep their own shape (social-hook is 9:16, the rest 16:9).
- **Layers** for anything custom (or on top of a template): text, shapes, photos and videos. Positions and sizes are fractions of the frame, measured at the layer's centre (x 0.5, y 0.5 = middle); the first layer is at the back. Give each layer an entrance (fade, slide up, slide left, scale pop, rotate, 3D flip), optionally an exit (fade out) and a loop (pulse, float) for the one thing that should keep moving.
- Good motion design is simple: one idea per screen, big readable text, 2–3 colours, things entering one after another (stagger the start times by about 0.2–0.4 s), and a calm last second.
- Use the user's own images through "generation:<id>" or an upload link, exactly like other files.
- Changes? Call `create_motion_design` again with the whole new version.

## 6. Templates

Templates are ready-made looks by creators: the user adds their photo and gets that look; video templates rebuild a whole edited video step by step. Use `search_templates` / `get_template` to find one and explain what it needs, then give the user the template link — templates are used on pyplex.com. Template prompts are private; never ask for or guess them.

## 7. Account questions

- Balance → `get_balance` (shows a wallet card with Add funds).
- "What did I make?" / reuse something → `list_my_generations`, then `generation:<id>`.
- How Pyplex works, pricing, refunds, payouts → `read_docs` (page list without arguments).
- Creators and earnings → [references/creators.md](references/creators.md).

## 8. When something goes wrong

| What you see | What to do |
| --- | --- |
| HTTP sign-in / "Sign in to Pyplex" | The app shows Connect; ask the user to press it and Allow, then retry the same step |
| `enough_balance: false` / "Not enough balance" | Give `top_up_url`; wait for them to top up; quote again |
| "quote expired" (after 10 minutes) | Quote again and get a new yes for the new price |
| "not a valid setting" / missing field | `get_model` again and fix the setting — never guess option values |
| Safety filter blocked it | Not charged. Suggest a different wording; don't try to get around the filter |
| "4 generations are already running" / daily limit | Wait for one to finish / try tomorrow |
| Upload link has no file yet | Ask the user to finish on the upload page; `check_upload` with `wait_seconds` |
| Edit link says "wasn't found" | They're signed in to a different Pyplex account in that browser — sign in with the one connected here |
| Editor says a file couldn't be downloaded | Uploaded files are kept 30 days; make the edit again (re-upload if needed) |
| `create_video_edit` / `create_motion_design` lists problems | Fix exactly those fields and call it again |

## Never

- Start a generation without a fresh yes for that exact price.
- Reveal or guess a template's hidden prompt.
- Help make content that impersonates a real person without their consent, sexual content involving minors, or anything Pyplex's rules forbid (`read_docs` page `rules`). Voice cloning needs the voice owner's permission.
