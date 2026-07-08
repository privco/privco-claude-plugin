# PrivCo Data — Claude Code plugin

One-step install of the **PrivCo MCP server** (17 tools for private-company
search, profiles, financials, funding, deals, and contacts) together with the
**PrivCo search skill** that teaches Claude the non-obvious filter semantics
and multi-tool workflows.

## Install (Claude Code)

```
/plugin marketplace add privco/privco-claude-plugin
/plugin install privco-data@privco
```

When you enable the plugin, Claude Code prompts for your **PrivCo API key**
(masked; stored in your system keychain, never written to config files).
Contact <support@privco.com> if you don't have one.

That's it — the MCP server runs on demand via `npx privco-data-mcp`, and the
skill auto-activates on PrivCo-flavored requests ("find companies that…",
"look up <company> in PrivCo", "valuations for…").

Non-interactive (scripts / CI):

```bash
claude plugin marketplace add privco/privco-claude-plugin
claude plugin install privco-data@privco
```

Requires Node.js ≥ 18 (for the npm-hosted MCP server).

## What's inside

| Component | What it gives you |
|---|---|
| `.mcp.json` | Registers the [`privco-data-mcp`](https://www.npmjs.com/package/privco-data-mcp) stdio MCP server (17 tools), keyed by your API key |
| `skills/privco-mcp-search/` | The [PrivCo search skill](https://github.com/privco/privco-mcp-search-skill): tool inventory, filter gotchas, and standard workflows. The deep per-tool reference and guided prompts (including the company-intelligence dashboard) ship inside the MCP server itself, as `privco://docs/*` resources and built-in prompts |

## Prefer the hosted connector instead?

If you'd rather not run anything locally, PrivCo also hosts a **remote MCP
connector** at `https://mcp.privco.com/mcp` (OAuth sign-in with your PrivCo
account — no API key). It works in claude.ai, Claude Desktop, Claude Code,
and ChatGPT. See the skill's
[INSTALL.md](https://github.com/privco/privco-mcp-search-skill/blob/main/INSTALL.md)
for per-client steps. Use one or the other — both expose the same 17 tools.

Note for claude.ai / Claude Desktop **chat** users: plugins there carry only
the bundled skill (local MCP servers don't run in chat) — pair the skill with
the remote connector.

## Maintenance

The skill content under `skills/privco-mcp-search/` mirrors the
[`privco-mcp-search-skill`](https://github.com/privco/privco-mcp-search-skill)
repo — that repo is the source of truth; sync it here when it changes and
bump `version` in `.claude-plugin/plugin.json` so installed copies update.

## License

[MIT](./LICENSE)
