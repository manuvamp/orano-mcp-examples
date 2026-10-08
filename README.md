# ORANO personal MCP — curl examples

Minimal, copy-paste examples for reading your own ORANO library through the personal, read-only MCP server. No SDK required.

- Endpoint & auth format: https://oranoai.com/mcp.json
- Overview: https://oranoai.com/mcp
- Key management: https://oranoai.com/mcp-access.html

## Setup

```bash
BASE="https://orano-ai-backend-1037939693300.us-central1.run.app/mcp/"
KEY="YOUR_ORANO_PERSONAL_KEY"   # generate at oranoai.com/mcp-access.html (subscription required)
```

## 1. Initialize the session

```bash
curl -s -X POST "$BASE" \
  -H "Authorization: Bearer $KEY" \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -d '{"jsonrpc":"2.0","id":1,"method":"initialize","params":{"protocolVersion":"2025-03-26","capabilities":{},"clientInfo":{"name":"curl","version":"1.0"}}}'
```

Copy the `mcp-session-id` response header into `SID` for later calls:

```bash
SID="PASTE_SESSION_ID"
```

## 2. List your projects

```bash
curl -s -X POST "$BASE" -H "Authorization: Bearer $KEY" -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" -H "mcp-session-id: $SID" \
  -d '{"jsonrpc":"2.0","id":2,"method":"tools/call","params":{"name":"list_projects","arguments":{}}}'
```

## 3. Search your library

```bash
curl -s -X POST "$BASE" -H "Authorization: Bearer $KEY" -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" -H "mcp-session-id: $SID" \
  -d '{"jsonrpc":"2.0","id":3,"method":"tools/call","params":{"name":"search_library","arguments":{"query":"pgvector"}}}'
```

## 4. Read curated memory facts

```bash
curl -s -X POST "$BASE" -H "Authorization: Bearer $KEY" -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" -H "mcp-session-id: $SID" \
  -d '{"jsonrpc":"2.0","id":4,"method":"tools/call","params":{"name":"get_memory_facts","arguments":{}}}'
```

## Available tools

`list_projects` · `get_project` · `get_pending_handoffs` · `search_library` · `get_memory_facts`

## Boundaries

Read-only (scope `orano:read`), personal keys, 240 calls / 60 min budget, up to 10 active keys. No OAuth yet — keys are provisioned manually after subscribing.

ORANO app: [iOS](https://apps.apple.com/us/app/orano-ai/id6791454509) · [Android](https://play.google.com/store/apps/details?id=com.oranoai.app) · [oranoai.com](https://oranoai.com)

## Listed in the Official MCP Registry

This server is published in the official MCP Registry: **`io.github.manuvamp/orano-personal-context-mcp`** (streamable-http). Browse it at https://registry.modelcontextprotocol.io or search there for "orano". Also listed on mcpservers.org.

Quick check that the registry knows the server:

```bash
curl "https://registry.modelcontextprotocol.io/v0.1/servers?search=orano"
```

## Setup guides

- [Claude Code](https://oranoai.com/blog/connect-orano-claude-code-mcp.html): one `claude mcp add --transport http` command, or a `.mcp.json` with an env-var key
- [Cursor](https://oranoai.com/blog/connect-orano-cursor-mcp.html): `mcp.json` with `url` + `Authorization: Bearer ${env:ORANO_MCP_KEY}`
- [Three ways to use saved videos in ChatGPT, Claude or Cursor](https://oranoai.com/blog/give-chatgpt-claude-your-saved-videos.html)
- Machine-readable connection details: https://oranoai.com/mcp.json
