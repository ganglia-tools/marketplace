---
description: One-shot onboarding for an unfamiliar repo using Ganglia.
allowed-tools: mcp__ganglia__code_overview, mcp__ganglia__code_summary, mcp__ganglia__code_hotspots, mcp__ganglia__code_memory
---

You're entering a new project. Run this sequence and report back to the user concisely:

1. `code_overview()` — confirm the graph is indexed (files, functions, edges).
2. `code_summary()` — pull the project shape.
3. `code_hotspots(type="called", limit=10)` — find the 10 most-called functions (the load-bearing code).
4. `code_memory(action="recall", text="project context decisions preferences", limit=5)` — surface anything saved from prior sessions.

Then synthesize ONE paragraph for the user covering: what the project is, the most critical functions to know about, and any prior decisions worth remembering. Don't dump raw tool output — paraphrase.

If `code_overview` returns 0 nodes, tell the user to run `gng watch . &` and stop — you can't help until the graph is indexed.
