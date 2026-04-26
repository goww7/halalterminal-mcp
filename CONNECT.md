# Connecting to the Halal Terminal MCP server

## Endpoint

```
https://mcp.halalterminal.com/sse
```

- Transport: **SSE** (Server-Sent Events)
- Auth: `X-API-Key: <your_key>` header, or `?api_key=<your_key>` query param
- Get a key (free, no credit card): https://api.halalterminal.com

---

## Claude Code

### Option A — direct SSE (recommended)

```bash
claude mcp add --transport sse halalterminal \
  https://mcp.halalterminal.com/sse \
  --header "X-API-Key: ht_yourkey"
```

### Option B — project-scoped via `.mcp.json`

```json
{
  "mcpServers": {
    "halalterminal": {
      "type": "sse",
      "url": "https://mcp.halalterminal.com/sse",
      "headers": { "X-API-Key": "ht_yourkey" }
    }
  }
}
```

> Prefer the [`halalterminal-claude-skills`](https://github.com/goww7/halalterminal-claude-skills) plugin — it ships a `/halal-setup` slash command that handles this for you.

---

## Claude Desktop

Edit `claude_desktop_config.json` (Settings → Developer → Edit Config) and add the bridge below. Claude Desktop currently expects stdio, so we use the official SSE → stdio relay.

```json
{
  "mcpServers": {
    "halalterminal": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-everything-sse-bridge",
        "https://mcp.halalterminal.com/sse"
      ],
      "env": {
        "MCP_HEADER_X_API_KEY": "ht_yourkey"
      }
    }
  }
}
```

If your client doesn't support that bridge, use the snippet under **Custom stdio bridge** below.

---

## Cursor

Cursor → Settings → MCP → *New MCP server*:

```json
{
  "mcpServers": {
    "halalterminal": {
      "url": "https://mcp.halalterminal.com/sse?api_key=ht_yourkey"
    }
  }
}
```

---

## Windsurf

Windsurf → Settings → Cascade → MCP servers:

```json
{
  "mcpServers": {
    "halalterminal": {
      "serverUrl": "https://mcp.halalterminal.com/sse",
      "headers": { "X-API-Key": "ht_yourkey" }
    }
  }
}
```

---

## Custom stdio bridge

For any MCP client that requires stdio, drop this 20-line bridge alongside your config and point the client at it.

`halalterminal-mcp.mjs`:

```js
import { SSEClientTransport } from "@modelcontextprotocol/sdk/client/sse.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

const API_KEY = process.env.HALALTERMINAL_API_KEY;
const sseUrl  = `https://mcp.halalterminal.com/sse?api_key=${API_KEY}`;

const sse   = new SSEClientTransport(new URL(sseUrl), {
  requestInit: { headers: { "X-API-Key": API_KEY } }
});
const stdio = new StdioServerTransport();

await sse.start();
await stdio.start();

stdio.onmessage = (m) => sse.send(m);
sse.onmessage   = (m) => stdio.send(m);
sse.onclose     = () => process.exit(0);
stdio.onclose   = () => process.exit(0);
sse.onerror     = (e) => { console.error("SSE error:", e); process.exit(1); };
```

Install once:

```bash
npm install -g @modelcontextprotocol/sdk
```

Use it from any stdio-only client config:

```json
{
  "mcpServers": {
    "halalterminal": {
      "command": "node",
      "args": ["/absolute/path/to/halalterminal-mcp.mjs"],
      "env": { "HALALTERMINAL_API_KEY": "ht_yourkey" }
    }
  }
}
```

---

## Verifying the connection

After connecting, ask your assistant:

> *"List the available halalterminal tools."*

You should see all 22 tools. Then try:

> *"Is AAPL halal?"*

If the call fails with `401`, the API key is missing or invalid. `403` means the key was deactivated. Check https://halalterminal.com/dashboard.

---

## Authentication details

| Method | Where |
|---|---|
| Header | `X-API-Key: ht_...` |
| Query string | `?api_key=ht_...` |

The server validates each request against the Halal Terminal API-key registry. The owning key is propagated to every tool call so per-user data (watchlists, screening cache) is correctly scoped.

## Plans

| Plan | Tokens / month | Price |
|---|---|---|
| Free | 50 | $0 |
| Starter | 2,500 | $19 |
| Pro | 15,000 | $49 |
| Enterprise | Unlimited | $199+ |

Upgrade: https://halalterminal.com/pricing
