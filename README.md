# @engram/mcp-server

MCP (Model Context Protocol) server that exposes the [Engram](https://github.com/agent-memory/engram) memory API as tools for Claude Desktop and other MCP-compatible clients.

## Features

- **6 Tools**: `engram_remember`, `engram_recall`, `engram_search`, `engram_forget`, `engram_context`, `engram_observe`
- **2 Resources**: `engram://stats`, `engram://context`
- **1 Prompt**: `memory-aware-chat`
- **Security**: Input validation, rate limiting, TLS enforcement for remote backends
- **Offline-resilient**: Graceful degradation when Engram is unreachable
- **Zero disk footprint**: Stateless proxy — stores nothing locally

## Installation

```bash
npm install -g @engram/mcp-server
```

## Claude Desktop Configuration

Edit `~/Library/Application Support/Claude/claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "engram": {
      "command": "engram-mcp",
      "env": {
        "ENGRAM_API_KEY": "ek_your_api_key",
        "ENGRAM_USER_ID": "user_you",
        "ENGRAM_BASE_URL": "http://localhost:3001"
      }
    }
  }
}
```

## Environment Variables

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `ENGRAM_API_KEY` | ✅ | — | API key for Engram backend |
| `ENGRAM_USER_ID` | ✅ | — | User namespace ID |
| `ENGRAM_BASE_URL` | ❌ | `http://localhost:3001` | Engram API URL |
| `ENGRAM_TIMEOUT_MS` | ❌ | `10000` | Request timeout (ms) |
| `ENGRAM_LOG_LEVEL` | ❌ | `warn` | `debug` / `info` / `warn` / `error` |
| `ENGRAM_MAX_RETRIES` | ❌ | `2` | Retry count for transient failures |
| `ENGRAM_TLS_SKIP_VERIFY` | ❌ | `false` | Skip TLS verification (dev only) |

## Tools

| Tool | Description |
|------|-------------|
| `engram_remember` | Store a memory for long-term recall |
| `engram_recall` | Semantic search across memories |
| `engram_search` | Entity/graph-aware search |
| `engram_forget` | Delete a memory by ID |
| `engram_context` | Generate an LLM-optimized context window |
| `engram_observe` | Auto-extract memories from text |

## Development

```bash
npm install
npm run build
npm test

# Run locally
ENGRAM_API_KEY=test ENGRAM_USER_ID=dev npm run dev
```

## License

MIT
