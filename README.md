# Vythos MCP Server

[![mcptry](https://mcptry.com/badge/tech.vythos/mcp)](https://mcptry.com/servers/tech.vythos/mcp)

Official MCP (Model Context Protocol) documentation and client configuration for **[Vythos](https://vythos.tech)** — the shared client Playbook and context layer for freelancers, consultants, and small agencies that syncs client rates, rules, and past work directly into Claude, ChatGPT, Copilot, Gemini, and Cursor.

* **Full Documentation & Setup Guides:** [https://doc.vythos.tech](https://doc.vythos.tech)
* **Get Started (Free for 1 client, no card required):** [https://vythos.tech](https://vythos.tech)

---

## Why Vythos MCP?

* **Task-Specific Context (`get_context`):** Sends only the client rules, day rates, payment terms, and past work each task needs — cutting AI token costs and rework.
* **Pre-Delivery Verification (`check_draft`):** Audits quotes, proposals, and client copy against your Playbook rules before you send them.
* **One Playbook Across Every Tool:** Connect Google Drive, Notion, Gmail, Slack, Harvest, and Fireflies once; use the same live context across Claude, ChatGPT, Cursor, Copilot, and Gemini.
* **Hosted & Zero-Setup:** Connects directly via Vythos's remote MCP endpoint — Streamable HTTP transport.

---

## Quick Setup

Everything you need is on the **AI tools** page in your Vythos workspace: the
server address, a key, and a ready-made snippet per tool. Full guide:
[doc.vythos.tech/ai-tools/connect](https://doc.vythos.tech/ai-tools/connect).

### Claude Desktop / ChatGPT / Gemini (OAuth — no key needed)

1. In Vythos, open **AI tools** and copy the server address.
2. In your tool, add a custom connector / MCP server and paste the address.
3. Sign in to Vythos in the browser and approve.

No API key required — these tools sign in with your Vythos account via OAuth.

### Cursor / Windsurf

Create or edit `.cursor/mcp.json` (or `~/.codeium/windsurf/mcp_config.json`):

```json
{
  "mcpServers": {
    "vythos": {
      "url": "https://api.vythos.tech/api/mcp/sse",
      "headers": { "Authorization": "Bearer <your-key>" }
    }
  }
}
```

### GitHub Copilot (VS Code)

Create or edit `.vscode/mcp.json`:

```json
{
  "servers": {
    "vythos": {
      "type": "http",
      "url": "https://api.vythos.tech/api/mcp/sse",
      "headers": { "Authorization": "Bearer <your-key>" }
    }
  }
}
```

### Claude Code

```bash
claude mcp add --transport http vythos https://api.vythos.tech/api/mcp/sse \
  --header "Authorization: Bearer <your-key>"
```

Use `--transport http`. The address ends in `/sse` for historical reasons, but
the server speaks Streamable HTTP — `--transport sse` fails to connect.

### Any other MCP client

| | |
|---|---|
| **Server URL** | From the AI tools page in Vythos |
| **Transport** | Streamable HTTP (POST) |
| **Auth** | OAuth (Claude, ChatGPT, Gemini) or `Authorization: Bearer <key>` (everything else) |

Generate and revoke per-tool API keys on the **AI tools** page in Vythos.

---

## Core MCP Tools

| Tool | Purpose | When to Call |
|------|---------|--------------| 
| `get_context` | Retrieve Playbook rules + personal memory | BEFORE any governed task |
| `search_memory` | Search for specific evidence/history; `exact=true` for exact words | For discovery/fact-finding |
| `read_source` | The whole of a source search found | Before quoting, or to read the rest of a thread |
| `list_sources` | What exists, newest first | "What do we have on this client?" |
| `check_draft` | Check a draft's rules, figures and client against what a pack handed over | BEFORE showing a draft |
| `log_outcome` | Record decisions/outcomes (evidence, never a rule) | AFTER completing a task |
| `save_to_playbook` | Propose a rule or a client fact, for a person to add | When the person asks to keep something |

---

## Documentation & Support

* **Docs & Setup Guides:** [https://doc.vythos.tech](https://doc.vythos.tech)
* **Website & Dashboard:** [https://vythos.tech](https://vythos.tech)

---

## License

[MIT](./LICENSE) — covers the configuration files in this repository only, not
the Vythos name, logo, or service.
