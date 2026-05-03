---
description: Codebase health snapshot — overview, dead code, cycles, duplicates.
allowed-tools: mcp__ganglia__code_overview, mcp__ganglia__code_dead, mcp__ganglia__code_cycles, mcp__ganglia__code_duplicates, mcp__ganglia__code_breaking_changes
---

Run a fast health check on the current project. Each call is independent — make them in parallel.

1. `code_overview()` — counts.
2. `code_dead(limit=20)` — top unreachable functions.
3. `code_cycles()` — file-level dependency cycles.
4. `code_duplicates(min_lines=15)` — copy-paste candidates worth refactoring.

Report a one-page summary in this exact shape:

```
🩺 HEALTH — <project>
─────────────────────────
size:       <files> files / <fns> functions / <classes> classes
dead code:  <N> unreferenced functions  (top: …)
cycles:     <N> SCCs across <M> files   (worst: …)
duplicates: <N> clone groups            (largest: <K> functions, <L> lines each)

verdict:    <one short sentence>
```

Verdict line: clean / minor / needs attention / critical, with a one-clause reason. No marketing language.
