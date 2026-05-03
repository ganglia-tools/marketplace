---
name: gng-safe-refactor
description: Use whenever the user asks to rename a symbol, reshape an API signature, or apply the same edit across many files. Forces the propagate → apply_batch → verify chain so the refactor is transactional and revertable, instead of falling back to many individual Edit() calls. Critical for changes touching more than 3 files.
---

# Safe multi-file refactor with Ganglia

You have access to the Ganglia MCP toolchain. When the user asks to rename a symbol, change an API's argument shape, or sweep the same edit across many files, you MUST use this chain instead of calling `Edit()` repeatedly. The chain is:

1. **Read the impact.** Call `code_impact(name="<symbol>", depth=2)`. Surface CRITICAL/HIGH dependents to the user. If the count is large or the change is risky, ask the user to confirm before proceeding.

2. **Find every match.** Call `code_propagate(symbol="<symbol>")`. This returns:
   - `callsites` — every call site with full context, line, col, current call text.
   - `definitions` — where the symbol is defined.
   - `mentions` — comments, strings, and indirect calls (`.bind`, `.apply`, `.call`).
   - `import_lines` — the import line in each file that referenced the symbol.

3. **Plan the edits.** Build the `edits` array for `code_apply_batch`. Each entry needs `{file, line, old, new}`. Source `old` from `current_call`; construct `new` based on the user's requested transformation. By default, IGNORE `mentions` of kind `in_string` and `in_comment` — comments and string literals are user-facing prose and should not be silently rewritten. If the user explicitly opts in, include them.

4. **Apply transactionally.** Call `code_apply_batch(message="<short description>", edits=[...], verify=true)`. The `verify` flag re-parses each touched file with tree-sitter and auto-reverts the whole batch if any new syntax errors appear.

5. **Confirm and offer rollback.** Report `op_id`, file count, and verify status. Always end with the literal revert command:

   ```
   To undo: code_revert(op_id="<op_id>")
   ```

## Hard rules

- **Never use Edit() for this.** A 47-file rename via 47 `Edit()` calls is half-applied if anything goes wrong, and there's no rollback. The whole point of this skill is the transactional guarantee.
- **Never skip step 1 (`code_impact`).** A "harmless" rename can break a CRITICAL dependent.
- **Never silently rewrite comments or strings.** Surface them in your report ("4 mentions in comments / 1 in a string — leaving them. Want me to update them too?").
- **If `code_apply_batch` returns `verified: verify_failed_reverted`**, do NOT retry. Tell the user the verify failed and what the parse error was. Wait for their input.
- **One refactor at a time.** If the user asks for two unrelated renames, run the chain twice — separate `op_id`s give them independent rollback.

## When NOT to use this skill

- Single-file edit → just use `Edit()` directly. The batch overhead isn't worth it.
- The user wants to *think* about a change, not apply it → call `code_impact` and `code_propagate` only, skip `code_apply_batch`.
- The user is editing user-facing copy (translations, error messages) — those are content, not refactors.
