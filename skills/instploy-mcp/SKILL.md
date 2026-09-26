---
name: instploy-mcp
description: Connect and use InstPloy MCP in Cursor. When the user enables InstPloy, says connect InstPloy, or pastes instploy url/Authorization JSON, run the connect-instploy flow first, then use InstPloy tools.
---

# InstPloy MCP (Cursor)

## First-time / reconnect

If InstPloy tools are missing, failing auth, or the user wants to connect:

1. Run the **connect-instploy** command (`/connect-instploy`)
2. Ask them to paste JSON like:

```json
"instploy": {
  "url": "https://YOUR_INSTANCE.instploy.com/instploy/manager/mcp",
  "headers": {
    "Authorization": "Bearer YOUR_TOKEN_HERE"
  }
}
```

3. Write `mcpServers.instploy` into `~/.cursor/mcp.json` and tell them to reload MCP
4. Or set the same values under **Plugins → InstPloy → Configure** (`INSTPLOY_URL`, `INSTPLOY_TOKEN`)

Never invent URL or token values. Never echo the full token — mask it (first 8 chars + `…`).

## After connected

- Prefer InstPloy MCP tools for remote workspace, Odoo install/upgrade, terminals, and deploy tasks
- Confirm the target instance before restart/upgrade/delete
- Never commit Bearer tokens to a repo
