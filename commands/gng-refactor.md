---
description: Safe rename or API reshape using propagate → apply_batch → verify (revertable).
argument-hint: <old-name> <new-name>
allowed-tools: mcp__ganglia__code_propagate, mcp__ganglia__code_apply_batch, mcp__ganglia__code_revert, mcp__ganglia__code_verify_edit, mcp__ganglia__code_history, mcp__ganglia__code_impact
---

The user wants to rename `$1` → `$2` (or reshape `$1`'s API to `$2`).

Run this chain:

1. `code_impact(name="$1", depth=2)` — quick blast-radius read. If anything is CRITICAL, surface it and ask the user to confirm before continuing.
2. `code_propagate(symbol="$1")` — get every callsite, definition, indirect call, and comment/string mention as classified JSON.
3. **Show the user a summary** of what was found (callsites count, definitions, indirect, mentions). Ask whether to proceed.
4. On confirmation, build the edits array — for each callsite, replace `$1` with `$2` preserving call shape. Skip `in_comment` and `in_string` mentions unless the user explicitly opts in.
5. `code_apply_batch(message="rename $1 → $2", edits=[...], verify=true)`.
6. Report the `op_id` and remind the user: `code_revert(op_id="…")` undoes the whole batch in one call.

If verify fails, tell the user it auto-reverted and surface the parse errors. Do NOT retry without their input.

If `code_propagate` returns the wrong file's definition (ambiguous symbol), use the `file:` parameter to disambiguate.
