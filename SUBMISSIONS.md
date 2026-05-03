# Distribution submissions — copy-paste reference

Status checklist. Tick each as you submit.

- [ ] mcp.so
- [ ] smithery.ai
- [ ] glama.ai
- [ ] modelcontextprotocol/servers (skip until 20+ stars)

---

## mcp.so

**Where:** <https://mcp.so/submit> (web form)
Or PR to: <https://github.com/chatmcp/mcp-directory>

**Fields:**

| Field | Value |
|---|---|
| Name | `Ganglia` |
| Slug | `ganglia` |
| Description (short) | Code-graph MCP server with 73 semantic tools that replace Read/Grep/Glob and slash token usage on real codebases. |
| Description (long) | Ganglia indexes your project into a call graph and exposes 73 semantic tools — code_get, code_callers, code_impact, code_propagate, code_apply_batch with one-click revert, code_safe_move, deliberation chain, smart LLM-backed digests, cross-session memory, and more. Works with Claude Code, Cursor, Windsurf, Continue, Cline, Goose. Languages: TypeScript, JavaScript, Rust, Python, Go, PHP. Free during public beta. |
| Repository | https://github.com/ganglia-tools/marketplace |
| Homepage | https://ganglia.dev |
| Install command | `npx -y -p @ganglia/cli gng mcp -p .` |
| Tags | `code-graph`, `refactoring`, `mcp`, `ai-agents`, `tree-sitter`, `call-graph`, `memory` |
| License | UNLICENSED (commercial; free during beta) |
| Author | Moado |
| Logo | https://ganglia.dev/favicon.svg |

---

## smithery.ai

**Where:** <https://smithery.ai/new>

Smithery auto-discovers from `smithery.yaml` (already in this repo's root).

**Fields:**

| Field | Value |
|---|---|
| Repository URL | https://github.com/ganglia-tools/marketplace |
| Display name | Ganglia |
| One-liner | Code-graph MCP server with 73 tools — replace Read/Grep/Glob, slash token usage. |
| Category | Developer Tools |
| Tags | code-graph, refactoring, mcp, ai-agents |

After submission, smithery will offer a 1-click install across all major MCP clients using the configSchema in `smithery.yaml`.

---

## glama.ai

**Where:** <https://glama.ai/mcp/servers/submit>

Often auto-indexes from mcp.so, but submit manually for faster listing.

**Fields:**

| Field | Value |
|---|---|
| Server name | Ganglia |
| GitHub URL | https://github.com/ganglia-tools/marketplace |
| Description | 73-tool code-graph MCP server. Indexes your repo into a call graph; exposes semantic tools that replace Read/Grep/Glob with 80–95% fewer tokens. Transactional cross-file refactor with one-click revert. Cross-session memory. Works with every major MCP client. |
| Categories | Developer Tools, Code Analysis |

---

## modelcontextprotocol/servers (Anthropic's official list)

**Where:** PR to <https://github.com/modelcontextprotocol/servers>

**Skip until you have 20+ GitHub stars and visible community traction.** They reject low-traction submissions to keep the list curated. Come back after a few months of mcp.so / smithery exposure.

When ready, the PR adds an entry to the README.md table:

```markdown
| **[Ganglia](https://github.com/ganglia-tools/marketplace)** | 73-tool code-graph server: call graph, transactional refactor, cross-session memory. |
```

---

## Tracking

After listings go live, expected traffic sources (in order of volume):
1. mcp.so (community discovery)
2. smithery.ai (1-click install funnel)
3. glama.ai (curated audience)
4. Direct GitHub search

Watch `npm view @ganglia/cli downloads` for week-over-week growth.
