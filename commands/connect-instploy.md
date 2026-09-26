---
name: connect-instploy
description: Connect InstPloy MCP by pasting your instploy JSON (url + Authorization Bearer). Use when enabling the InstPloy plugin or when the user says connect InstPloy.
---

# Connect InstPloy

## Goal

Ask the user for their InstPloy MCP JSON, parse it, and connect Cursor to that MCP server.

## Step 1 — Ask for JSON

Ask the user (in their language) to paste a config like this:

```json
"instploy": {
  "url": "https://YOUR_INSTANCE.instploy.com/instploy/manager/mcp",
  "headers": {
    "Authorization": "Bearer YOUR_TOKEN_HERE"
  }
}
```

Accept any of these shapes:

- The `instploy` object only
- Wrapped as `{ "instploy": { ... } }`
- Wrapped as `{ "mcpServers": { "instploy": { ... } } }`

## Step 2 — Parse

From the pasted JSON extract:

1. `url` — required string, must start with `http`
2. Bearer token — from `headers.Authorization`
   - If value is `Bearer xxx`, keep `xxx` only
   - If value has no `Bearer` prefix, use it as-is

If `url` or token is missing, ask again. Do not invent values.

## Step 3 — Connect (write user MCP config)

Update the user's global MCP file at `~/.cursor/mcp.json`:

1. Read the file if it exists; otherwise start from `{ "mcpServers": {} }`
2. Set / replace only the `mcpServers.instploy` entry:

```json
"instploy": {
  "url": "<parsed-url>",
  "headers": {
    "Authorization": "Bearer <parsed-token>"
  }
}
```

3. Keep every other MCP server unchanged
4. Write valid JSON (2-space indent)
5. Do not print the full token back in the chat — confirm with a short masked form (first 8 chars + `…`)

## Step 4 — Confirm

Tell the user:

1. InstPloy MCP was saved to `~/.cursor/mcp.json`
2. Reload Cursor or toggle MCP InstPloy off/on in **Customize → MCP**
3. Optional for marketplace plugin variables: set the same `url` and token under **Plugins → InstPloy → Configure** (`INSTPLOY_URL`, `INSTPLOY_TOKEN`)

## Security

- Never commit the pasted JSON or token to a repo
- Never store the token inside the plugin files
- Prefer masking the token in replies
