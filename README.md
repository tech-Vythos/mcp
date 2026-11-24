# Vythos MCP Server

Official MCP (Model Context Protocol) documentation and client configuration for **[Vythos](https://vythos.tech)** — the shared client Playbook and context layer for freelancers, consultants, and small agencies that syncs client rates, rules, and past work directly into Claude, ChatGPT, Copilot, Gemini, and Cursor.

* **Full Documentation & Setup Guides:** [https://doc.vythos.tech](https://doc.vythos.tech)
* **Get Started (Free for 1 client, no card required):** [https://vythos.tech](https://vythos.tech)

---

## Why Vythos MCP?
* **Task-Specific Context (`get_context`):** Sends only the client rules, day rates, payment terms, and past work each task needs—cutting AI token costs and rework.
* **Pre-Delivery Verification (`check_draft`):** Audits quotes, proposals, and client copy against your Playbook rules before you send them.
* **One Playbook Across Every Tool:** Connect Google Drive, Notion, Gmail, Slack, Harvest, and Fireflies once; use the same live context across Claude, ChatGPT, Cursor, Copilot, and Gemini.
* **Hosted & Zero-Setup:** Connects directly via Vythos's remote MCP endpoint with per-tool API keys.

---

## Quick Setup

### One-Line CLI Install
```bash
npx add-mcp 'https://api.vythos.tech/api/mcp/sse'
```

*(Or point coding agents like Claude Code directly to https://vythos.tech/skill.md for guided setup.)*

### Manual Client Configuration (Claude Desktop / Cursor / Windsurf)

Generate an API key in your Vythos workspace and add the following to your MCP config file (see [doc.vythos.tech](https://doc.vythos.tech) for client-specific guides):

```json
{
  "mcpServers": {
    "vythos": {
      "url": "https://api.vythos.tech/api/mcp/sse",
      "headers": {
        "Authorization": "Bearer YOUR_VYTHOS_API_KEY"
      }
    }
  }
}
```

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
* **Security & Key Management:** Generate and revoke per-tool API keys anytime in Settings (see [doc.vythos.tech](https://doc.vythos.tech)).

---

## License

[MIT](./LICENSE)
