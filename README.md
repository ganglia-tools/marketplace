# Ganglia — code-graph MCP server

[![npm](https://img.shields.io/npm/v/@ganglia/cli)](https://www.npmjs.com/package/@ganglia/cli)
[![Site](https://img.shields.io/badge/site-ganglia.dev-blue)](https://ganglia.dev)
[![Docs](https://img.shields.io/badge/docs-ganglia.dev-green)](https://ganglia.dev/docs)

Ganglia is an [MCP](https://modelcontextprotocol.io) server that gives AI coding agents a real understanding of your codebase — not file contents, but **structure**: who calls what, what breaks if you touch X, where a route ends up in the database.

It indexes your project into a call graph and exposes semantic tools that replace `Read` / `Grep` / `Glob` and slash token usage on real codebases. Works with Claude Code, Cursor, Windsurf, Continue, Cline, Goose — any MCP-compatible client.

## What you get

| Category | Tools |
|---|---|
| **Reading** | `code_get`, `code_signature`, `code_files`, `code_toc`, `code_overview`, `code_summary`, `code_structure`, `code_search`, `code_grep`, `code_quick` |
| **Navigation** | `code_callers`, `code_callees`, `code_context`, `code_related`, `code_trace`, `code_imports` |
| **Analysis** | `code_impact`, `code_hotspots`, `code_dead`, `code_cycles`, `code_duplicates`, `code_breaking_changes`, `code_diff_context`, `code_changelog`, `code_map` |
| **Refactor (transactional)** | `code_propagate`, `code_apply_batch`, `code_revert`, `code_history`, `code_rename_symbol`, `code_safe_move`, `code_slice`, `code_verify_edit` |
| **Schema & routing** | `code_route`, `code_route_trace`, `code_schema`, `code_env`, `code_type`, `code_type_usages` |
| **Memory & knowledge** | `code_memory`, `code_knowledge`, `code_annotate`, `code_checkpoint`, `code_config` |
| **Build / test / lint** | `code_build`, `code_test`, `code_lint`, `code_exec` |
| **Deliberation** | `deliberation_start`, `deliberation_opinion`, `deliberation_status`, `deliberation_result` |
| **Smart (LLM-backed)** | `code_smart_read`, `code_smart_grep`, `code_smart_diff`, `code_smart_context` |
| **Doc graph** | `doc_index`, `doc_list`, `doc_toc`, `doc_query`, `doc_get` |

Full reference: [ganglia.dev/tools](https://ganglia.dev/tools) · Docs: [ganglia.dev/docs](https://ganglia.dev/docs)

## Install

### Claude Code (plugin marketplace)

```
/plugin marketplace add ganglia-tools/marketplace
/plugin install ganglia@ganglia
```

Includes 5 slash commands and an auto-triggered safe-refactor skill.

### Cursor

`~/.cursor/mcp.json`:
```json
{
  "mcpServers": {
    "ganglia": {
      "command": "npx",
      "args": ["-y", "-p", "@ganglia/cli", "gng", "mcp", "-p", "."]
    }
  }
}
```

### Windsurf

`~/.codeium/windsurf/mcp_config.json`:
```json
{
  "mcpServers": {
    "ganglia": {
      "command": "npx",
      "args": ["-y", "-p", "@ganglia/cli", "gng", "mcp", "-p", "."]
    }
  }
}
```

### Continue / Cline / Goose / any MCP client

Same shape — point at the `gng mcp -p .` command:
```bash
npx -y -p @ganglia/cli gng mcp -p .
```

### Direct binary install

```bash
npm install -g @ganglia/cli
gng register                 # wires Claude Code automatically
```

Or grab a platform binary from [npm](https://www.npmjs.com/package/@ganglia/cli) or the [download page](https://ganglia.dev/download).

## Activation

Free during public beta. One-time setup:

1. Sign up: <https://ganglia.dev/signup> (30 seconds, name + email)
2. Copy your key from <https://ganglia.dev/dashboard>
3. `gng login <your-key>`

Verify: `gng whoami` shows your tier.

## Why use it

| Without Ganglia | With Ganglia |
|---|---|
| AI reads whole files to find one function | `code_get("functionName")` — 40 lines instead of 800 |
| AI greps blindly across the tree | `code_grep("pattern", max_results=5)` — ranked, structured |
| AI guesses what breaks if it changes a function | `code_impact(name, depth=2)` — severity-scored dependents |
| Cross-file rename = 47 individual `Edit()` calls | `code_propagate` → `code_apply_batch` — one transaction, one revert |
| Every session starts from scratch | `code_memory` — persistent context across conversations |

Token savings on a real codebase: **80–95%** vs raw file-reading patterns.

## Languages

TypeScript · JavaScript · Rust · Python · Go · PHP

## Repo layout

```
.claude-plugin/
├── marketplace.json   # Marketplace declaration (one plugin: "ganglia")
├── plugin.json        # Plugin manifest, points at mcp.json
└── mcp.json           # MCP server: npx -y -p @ganglia/cli gng mcp -p .
commands/              # 5 Claude Code slash commands
skills/                # gng-safe-refactor skill
smithery.yaml          # Smithery.ai auto-discovery manifest
```

## Links

- Site: <https://ganglia.dev>
- Docs: <https://ganglia.dev/docs>
- Tools reference: <https://ganglia.dev/tools>
- npm: <https://www.npmjs.com/package/@ganglia/cli>
- AI install recipe: <https://ganglia.dev/INSTALL.md>

The Ganglia source lives in a private repo. This repo is the public-facing distribution — manifests, install instructions, and integration glue. Issues and feature requests welcome here.
