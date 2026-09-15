---
name: orchestrator-mcp-setup
description: Install and run the Glob.AI orchestrator MCP server (stdio) with an MCP_TOKEN minted in the console, to work with projects, goals, plans, runs, and artifacts.
---

# Glob.AI orchestrator MCP setup

## When to use this skill

Use it when a human has engaged Glob.AI (has a project and console access) and wants an MCP-compatible agent (Claude Code, Coda, Codex, …) to work against the Glob.AI orchestrator: list projects and goals, read and update plans and work items, start runs, and create artifacts.

## What exists today

The orchestrator MCP server is a **local stdio server** — there is no hosted HTTP/SSE MCP endpoint. Its card, including the full tool list, is at:

```
GET https://glob.ai/.well-known/mcp/server-card.json
```

## Credentials

Access requires an `MCP_TOKEN`. Tokens are minted by a signed-in human in the Glob.AI console (https://aipods.glob.ai) from a project's runner setup — there is no self-service or anonymous token issuance. Authentication on glob.ai is otherwise user-based SSO — see https://glob.ai/auth.md.

## Running the server

The console's runner setup produces a paste-able command for your agent runtime that exports `MCP_TOKEN` and starts the stdio server. The server needs:

- `ORCHESTRATOR_URL` — the orchestrator API base URL (provided by the console command)
- `MCP_TOKEN` — the token minted above

## Related resources

- Server card (tool list, transport): https://glob.ai/.well-known/mcp/server-card.json
- Authentication overview: https://glob.ai/auth.md