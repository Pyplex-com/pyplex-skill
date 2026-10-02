# Pyplex for AI assistants

Make images, videos, music and voice with [Pyplex](https://pyplex.com)'s 900+ AI models straight from a conversation with Claude, ChatGPT, Cursor, Codex and other assistants.

Ask in your own words — *"put a red sports car behind me in this photo"*, then *"now make a video of me opening the door and sitting inside"*. Your assistant picks the right model, writes the prompt, shows you the **exact price**, and starts only after you say yes. The result appears in the chat (in apps that show Pyplex's card) and is saved in your Pyplex Library.

This plugin contains:

- **The Pyplex connector** (`.mcp.json`) — Pyplex's MCP server at `https://pyplex.com/api/mcp/account` (the same address in every app).
- **The `pyplex` skill** (`skills/pyplex/`) — teaches your assistant the Pyplex workflow: picking models, writing prompts, uploads, chaining results, editing clips into one video (opens in the Pyplex editor), motion graphics (opens in Pyplex Motion Design), prices and confirmation.

## Install

Source: [github.com/Pyplex-com/pyplex-skill](https://github.com/Pyplex-com/pyplex-skill) · Download: [pyplex.com/downloads/pyplex-plugin.zip](https://pyplex.com/downloads/pyplex-plugin.zip)

**Claude Code** — straight from GitHub:

```bash
claude plugin marketplace add Pyplex-com/pyplex-skill
claude plugin install pyplex@pyplex
```

Run `/mcp` and sign in to Pyplex when asked. (From the zip instead: unzip it to a folder and use `claude plugin marketplace add ./pyplex-plugin`.)

**Claude (web, desktop)** — Customize → Plugins → Add → Upload plugin, and pick `pyplex-plugin.zip`. Then open the plugin's **Connectors** tab and connect Pyplex.

**Codex** — unzip it to a folder, then:

```bash
codex plugin marketplace add ./pyplex-plugin
codex plugin add pyplex@pyplex
codex mcp login pyplex
```

Or only the connector: `codex mcp add pyplex --url https://pyplex.com/api/mcp/account` then `codex mcp login pyplex`.

**Other agents that support skills (Cursor, OpenCode and more)** — copy the `skills/pyplex` folder (from this repository or the zip) into your agent's skills folder. Add the connector in your app as an HTTP MCP server: `https://pyplex.com/api/mcp/account`, and sign in to Pyplex once when the app asks.

**Only the connector** — Claude: Customize → Connectors → Add custom connector → URL `https://pyplex.com/api/mcp/account`, Authentication **Sign in now**, OAuth client **Register automatically**, request headers empty → Add → sign in to Pyplex → **Allow** (once — it stays connected). Claude Code: `claude mcp add --transport http pyplex https://pyplex.com/api/mcp/account`. ChatGPT: the same address as a custom connector.

## How paying works

- You sign in to Pyplex and press **Allow** once, when you add the connector; the app stays connected. You can disconnect any time from your Pyplex Dashboard → Connected apps.
- Looking up models, prices, templates and docs is free.
- Every generation is two steps: a free price check, then your **yes** (or the **Generate** button on the Pyplex card). Nothing is charged without it.
- If your balance is low, you get a link to add money on Pyplex (minimum top-up $10). Failed generations are refunded automatically.
- Putting clips together into one video is free: you get an **Open in Editor** link, and exporting the finished video in the Pyplex editor costs a small fee from your balance.

## Data

The connector sends your requests (model, prompt, settings) and the files you choose to Pyplex, through `pyplex.com`, using your Pyplex account. Files you add through an upload link stay in your Pyplex account. The assistant never sees your password, email or payment details, and it can't top up or withdraw money. See [pyplex.com/privacy](https://pyplex.com/privacy) and [pyplex.com/docs/ai-assistants](https://pyplex.com/docs/ai-assistants).

## License

Apache-2.0 — see [LICENSE](LICENSE).
