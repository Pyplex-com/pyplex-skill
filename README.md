<div align="center">

# Pyplex for AI assistants

**Make images, videos, music and voice with 900+ AI models — right from your chat with Claude, ChatGPT, Codex, Cursor and other assistants.**

[Website](https://pyplex.com) · [Docs](https://pyplex.com/docs/ai-assistants) · [Download the plugin (zip)](https://pyplex.com/downloads/pyplex-plugin.zip)

![License: Apache-2.0](https://img.shields.io/badge/license-Apache--2.0-blue) ![MCP connector](https://img.shields.io/badge/MCP-connector-10b981) ![Price shown first](https://img.shields.io/badge/price-shown%20before%20you%20pay-6366f1)

</div>

---

## What you can ask

Talk in your own words. Your assistant picks the model, writes the prompt and shows the price first.

| You say | What happens |
| --- | --- |
| *"Put a red sports car behind me in this photo"* | Your photo is edited with a top photo model (for example Seedream 5.0 Pro or Nano Banana Pro) |
| *"Now make a 5-second video of me opening the door"* | That photo becomes a video (for example Seedance 2.5) |
| *"Cut my last three clips into a 15-second Reel with music"* | You get an **Open in Editor** link — everything is already on the timeline in the Pyplex video editor |
| *"Make an animated title card for my shop"* | It opens, ready to adjust, in **Pyplex Motion Design** |
| *"Make a 30-second upbeat track for my product video"* | Music or a voice-over from an audio model |

## How it works

1. **Ask** for what you want.
2. Your assistant **picks a model** and writes the prompt for you.
3. You see the **exact price** — nothing is charged yet.
4. Say **yes** (or press **Generate** on the Pyplex card).
5. The result appears **in the chat** and is saved in your **Pyplex Library**.

## Install

### Claude Code — straight from GitHub

```bash
claude plugin marketplace add Pyplex-com/pyplex-skill
claude plugin install pyplex@pyplex
```

Then run `/mcp` and sign in to Pyplex when asked.

### Claude (web and desktop)

1. Download [pyplex-plugin.zip](https://pyplex.com/downloads/pyplex-plugin.zip).
2. **Customize → Plugins → Add → Upload plugin**, and pick the zip.
3. Open the plugin's **Connectors** tab and connect Pyplex.

### Codex

Unzip the plugin to a folder, then:

```bash
codex plugin marketplace add ./pyplex-plugin
codex plugin add pyplex@pyplex
codex mcp login pyplex
```

### Cursor, OpenCode and other agents with skills

Copy the [`skills/pyplex`](skills/pyplex) folder into your agent's skills folder, then add the connector below.

### Only the connector

Every app uses the same address: `https://pyplex.com/api/mcp/account`

| App | How to add it |
| --- | --- |
| Claude | Customize → Connectors → Add custom connector → the address above, Authentication **Sign in now**, OAuth client **Register automatically**, no request headers → Add → sign in to Pyplex → **Allow** |
| Claude Code | `claude mcp add --transport http pyplex https://pyplex.com/api/mcp/account` |
| ChatGPT | Add a custom connector with the address above |
| Codex | `codex mcp add pyplex --url https://pyplex.com/api/mcp/account`, then `codex mcp login pyplex` |
| Cursor, VS Code, other MCP apps | Add an HTTP MCP server with the address above |

You sign in once, when you add it — the app stays connected.

## Paying and safety

- You sign in to Pyplex and press **Allow** once, when you add the connector. You can disconnect any time from your Pyplex **Dashboard → Connected apps**.
- Looking up models, prices, templates and docs is free.
- Every generation is two steps: a free price check, then your **yes**. Nothing is charged without it.
- If your balance is low, you get a link to add money on Pyplex (minimum top-up $10). Failed generations are refunded automatically.
- Putting clips together into one video is free. Exporting the finished video in the Pyplex editor costs a small fee from your balance, shown before you export.

## What's inside

| Path | What it is |
| --- | --- |
| [`skills/pyplex/`](skills/pyplex) | The skill: which model fits which job, how to write prompts, uploads, chaining a photo into a video, editing clips, motion graphics, and the price-and-yes rule |
| `.mcp.json`, `mcp.json` | The Pyplex connector (MCP server at `https://pyplex.com/api/mcp/account`) |
| `.claude-plugin/`, `.codex-plugin/`, `.cursor-plugin/`, `.agents/`, `plugin.json` | Plugin manifests for each app |

## Data

The connector sends your requests (model, prompt, settings) and the files you choose to Pyplex, through `pyplex.com`, using your Pyplex account. Files you add through an upload link stay in your Pyplex account. The assistant never sees your password, email or payment details, and it can't top up or withdraw money. See [pyplex.com/privacy](https://pyplex.com/privacy) and [pyplex.com/docs/ai-assistants](https://pyplex.com/docs/ai-assistants).

## License

Apache-2.0 — see [LICENSE](LICENSE).
