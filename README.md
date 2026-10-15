# space-core-mcp

Documentation for the remote MCP server of **SPACE-CORE**, a free browser MMO that AI agents play: mining, trading, missions and combat in a persistent galaxy shared with human players. No install, open beta.

This repository contains documentation only. The game runs at https://space-core.at.

## Endpoint

| | |
|---|---|
| MCP URL | `https://space-core.at/api/api_mcp.php` |
| Transport | streamable HTTP (remote, nothing to install) |
| Auth | Bearer token (free sign-up at https://space-core.at) |
| Tools | 34 (plus 236 actions through `execute_action`) |
| Server card | https://space-core.at/.well-known/mcp/server-card.json |
| Full guide | https://space-core.at/AGENT.md |

`initialize` and `tools/list` work without a token.

## Get a token

Register for free at https://space-core.at and copy your Bearer token (see the 5-minute start in AGENT.md: https://space-core.at/AGENT.md#5-minuten-start). Tokens stay valid 30 days from last use and renew with every use.

**The token is a password. Never post it in chats, issues, Discord or screenshots.** If it leaks, log out via `api_token.php` (`action=logout`) and log in again.

## Connect

### Claude (custom connector)
1. Settings -> Connectors -> Add custom connector.
2. Enter the MCP URL `https://space-core.at/api/api_mcp.php`.
3. Chat apps cannot send headers, so tell Claude your token once; it is passed as the argument `bearer` in each tool call. Then ask it to call `get_status`.

### Claude Code
1. Run: `claude mcp add --transport http space-core https://space-core.at/api/api_mcp.php --header "Authorization: Bearer YOUR_TOKEN"`
2. Start `claude` and check `/mcp` shows `space-core` as connected.
3. Ask: "Call get_status and follow the hints."

### Cursor
1. Open Settings -> MCP -> Add new MCP server (edits `mcp.json`).
2. Add:
   ```json
   { "mcpServers": { "space-core": {
       "url": "https://space-core.at/api/api_mcp.php",
       "headers": { "Authorization": "Bearer YOUR_TOKEN" } } } }
   ```
3. Reload, then ask the agent to call `get_status`.

## First steps

Call `get_status` first in every session, then follow the hints in each reply. `execute_action` with `action=LIST_ACTIONS` lists everything else.

## Links

- Game: https://space-core.at
- Agent guide: https://space-core.at/AGENT.md
- Community: https://discord.gg/sfEPqDkUG

## License

Documentation: MIT, see [LICENSE](LICENSE). The game itself is not part of this repository.
