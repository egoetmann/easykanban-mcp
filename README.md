# EasyKanban MCP Server

Connect Claude, ChatGPT, Cursor, or any MCP-compatible AI to your
[EasyKanban](https://easykanb.app) kanban boards. Ask for a to-do summary across
all your boards, then let your assistant create, update, and move cards for you.

**Endpoint:** `https://easykanb.app/api/mcp`
**Transport:** Streamable HTTP
**Auth:** OAuth 2.1 (PKCE + Dynamic Client Registration) — no API keys

## Setup

### Claude (web & desktop)

Settings → Connectors → **Add custom connector**, paste
`https://easykanb.app/api/mcp`, then click **Allow** in the browser window that
opens.

### Claude Code

```bash
claude mcp add --transport http easykanban https://easykanb.app/api/mcp
```

Then run `/mcp` to authenticate.

### ChatGPT

Settings → Connectors → **Add custom connector**, paste
`https://easykanb.app/api/mcp`, confirm the EasyKanban sign-in.

### Cursor, VS Code & other clients

```json
{
  "mcpServers": {
    "easykanban": {
      "url": "https://easykanb.app/api/mcp"
    }
  }
}
```

One-click install links for Cursor and VS Code are on
<https://easykanb.app/mcp>.

## Tools

Reading is free on every account. Writing requires
[EasyKanban Pro](https://easykanb.app/#pricing) (€6/month) and unlocks
immediately on upgrade — no reconnect needed.

| Tool | Plan | Description |
| --- | --- | --- |
| `list_boards` | Free | List all boards you can access |
| `get_board` | Free | Read a board with its columns, cards, and tag names |
| `list_cards` | Free | List and filter cards on a board |
| `get_todo_overview` | Free | Cross-board to-do summary sorted by due date |
| `create_card` | Pro | Create a card in a column |
| `update_card` | Pro | Edit title, description, tags, due date |
| `move_card` | Pro | Move a card between columns or positions |
| `archive_card` | Pro | Archive a card (reversible) |
| `delete_card` | Pro | Permanently delete a card |
| `create_board` | Pro | Create a board with a set of columns |
| `create_column` | Pro | Add a column to a board |

## Example prompts

- "What are my most important to-dos this week?"
- "Summarize everything that is overdue across my boards."
- "Create a card 'Send invoice to ACME' in my Freelance board."
- "Move the 'Design review' card to Done."
- "Add cards for all the action items from this meeting transcript."

## Security

- **Your existing login.** Authorization runs through OAuth against your
  EasyKanban account. No API keys or passwords are shared with the AI.
- **Same permissions as in the app.** Every request runs under your identity
  with Postgres row-level security applied, so your AI sees only boards you can
  access, and team roles (owner, editor, viewer) are enforced by the database.
- **Revoke anytime.** Settings → Connected Apps cuts off an app's access
  immediately.

## Links

- Setup & docs: <https://easykanb.app/mcp>
- Pricing: <https://easykanb.app/#pricing>
- Privacy: <https://easykanb.app/privacy>
