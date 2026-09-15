---
description: Documents CLI tools available for agent use in this environment and when to prefer them over their MCP equivalents. Use when deciding how to check deployment status, manage a project, configure environment variables, or perform any operation that has both a CLI command and an MCP tool.
---

# External Tools

Reference for CLI tools available in this environment, and when to use them instead of the equivalent MCP server tools.

## General rule: CLI vs MCP

- If you already know the exact operation you need, use the CLI directly. It's a single local command with no extra tool-call round trip.
- Fall back to the MCP server when you need to explore what's available, need structured/parseable output for further automation, or the operation isn't exposed by the CLI at all.

## Vercel

Use the Vercel CLI instead of the Vercel MCP tools whenever you already know which operation you need. Reach for Vercel MCP tools only for operations the CLI doesn't cover (e.g. web analytics, runtime error/log queries, domain purchases, toolbar threads).

| Task | Command | MCP equivalent to skip |
|---|---|---|
| Deployment status | `vercel ls` | `list_deployments`, `get_deployment` |
| Environment variables | `vercel env ls` | — |
| Project management | `vercel project ls`, `vercel project inspect <name>` | `list_projects`, `get_project` |

## Adding more CLIs

When a new CLI is installed, add a new `##` section above following the same pattern: what it's used for, when to prefer it over its MCP equivalent, and a quick-reference table of commands.
