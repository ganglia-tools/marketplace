# Ganglia — Claude Code plugin marketplace

This repo is the [Claude Code plugin marketplace](https://docs.claude.com/en/docs/claude-code/plugins) entry for **Ganglia** (`gng`).

It contains the plugin manifest only — the binary itself ships via npm (`@ganglia/cli`).

## Install

```
/plugin marketplace add ganglia-tools/marketplace
/plugin install ganglia@ganglia
```

That wires the `ganglia` MCP server into Claude Code via `npx -y -p @ganglia/cli gng mcp -p .`.

You still need a free activation key to actually run any `code_*` tool:

1. Sign up: https://ganglia.dev/signup (free, 30 seconds)
2. Copy your key: https://ganglia.dev/dashboard
3. Activate: `gng login <your-key>`

## What is Ganglia?

A code-graph MCP server that gives your AI assistant 70 specialized tools (`code_get`, `code_grep`, `code_callers`, `code_apply_batch`, `code_revert`, …) that replace `Read`/`Grep`/`Glob` and dramatically reduce token usage on real codebases.

- Full overview: https://ganglia.dev
- Tools reference: https://ganglia.dev/tools
- Docs: https://ganglia.dev/docs
- AI install recipe: https://ganglia.dev/INSTALL.md

## Repo layout

```
.claude-plugin/
├── marketplace.json   # Marketplace declaration (one plugin: "ganglia")
├── plugin.json        # Plugin manifest, points at mcp.json
└── mcp.json           # MCP server: npx -y -p @ganglia/cli gng mcp -p .
```

The Ganglia source lives in a private repo. This repo is intentionally manifest-only.
