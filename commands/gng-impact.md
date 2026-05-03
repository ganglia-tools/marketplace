---
description: What breaks if I change this symbol? Severity-scored blast radius.
argument-hint: <symbol>
allowed-tools: mcp__ganglia__code_impact, mcp__ganglia__code_callers, mcp__ganglia__code_test_for
---

The user wants to know the blast radius of changing `$ARGUMENTS`.

1. Call `code_impact(name="$ARGUMENTS", depth=2)`.
2. If the result has CRITICAL or HIGH-severity dependents, also call `code_test_for(name="$ARGUMENTS")` to surface the test files that would catch a regression.
3. Report:
   - **Total dependents** (count by severity).
   - **The 3 most critical paths** that would break.
   - **Test coverage** — which tests cover the symbol, or "no tests found".
4. End with a one-line recommendation: safe / proceed with care / needs deliberation first.

Do NOT propose any code change yet. The user can ask for that as a follow-up.
