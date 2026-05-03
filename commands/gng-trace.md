---
description: Trace an HTTP route end-to-end — controller → service → DB.
argument-hint: <route> [METHOD]
allowed-tools: mcp__ganglia__code_route_trace, mcp__ganglia__code_route, mcp__ganglia__code_schema, mcp__ganglia__code_env
---

The user wants to follow `$ARGUMENTS` from request to database.

1. Parse `$ARGUMENTS`. First token is the route (`/api/users`, `/login`, etc.). Optional second token is the HTTP method; default to `GET`.
2. Call `code_route_trace(route="<route>", method="<method>")` to get the full chain.
3. If the chain touches a DB query, call `code_schema()` to surface the relevant table(s).
4. If the handler reads env vars (look for `process.env`, `std::env::var`, `os.getenv`), call `code_env()` for the names referenced.

Report:
- The handler entry function (file:line).
- The chain of calls (controller → service → repository → query).
- Tables touched + key columns.
- Env vars consumed.

Keep it under 25 lines. Don't dump function bodies — just names and locations.
