# InstPloy Cursor Plugin

Installable Cursor plugin that connects to InstPloy MCP.

## What you get on install

Cursor asks you to configure two fields (same values as your JSON):

| Field | Maps to JSON |
|-------|----------------|
| `url` (`INSTPLOY_URL`) | `instploy.url` |
| `Authorization Bearer token` (`INSTPLOY_TOKEN`) | token from `headers.Authorization` |

Example JSON:

```json
"instploy": {
  "url": "https://YOUR_INSTANCE.instploy.com/instploy/manager/mcp",
  "headers": {
    "Authorization": "Bearer YOUR_TOKEN_HERE"
  }
}
```

## Paste JSON in chat (fastest)

After the plugin is loaded, run:

```text
/connect-instploy
```

Paste your `instploy` JSON. The agent writes it to `~/.cursor/mcp.json` and you reload MCP.

## Local install

```bash
cp -R . ~/.cursor/plugins/local/instploy
```

Then `Developer: Reload Window`.
