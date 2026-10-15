# Capability: building skills and MCP servers

## Writing a skill (for Antigravity or any skill-aware agent)

A skill is a folder with a `SKILL.md`:

```
my-skill/
  SKILL.md            required: frontmatter + instructions
  references/*.md     optional: loaded only when needed
  scripts/*           optional: deterministic helpers
```

Frontmatter:

```yaml
---
name: my-skill                  # lowercase, hyphens, matches the folder
description: When to use it and what it does, in one or two sentences.
---
```

The description is what triggers the skill, so write it as "Use when ..."
with the concrete situations and keywords a request would contain.

Principles:

- Keep `SKILL.md` lean (roughly 150-300 lines). Move depth to `references/` and
  say exactly when to load each file. This keeps context small.
- Instructions, not essays: imperative steps, decision tables, short examples.
- Put anything that must be exact in a script, not in prose.
- Explain the why behind a rule; models follow reasoned rules better than bare ones.
- Test it: run 3-5 realistic prompts with and without the skill, and compare
  results. Revise the description if it fires too often or not at all.

## Building an MCP server

1. **Pick the transport**: stdio for local tools, streamable HTTP for hosted ones.
2. **Design tools around tasks, not endpoints.** A tool should accomplish
   something the agent wants (`find_orders`, `refund_order`), not mirror every REST route.
3. **Naming and docs**: verb-first, unambiguous names; descriptions that say
   when to use the tool, what it returns, and what it cannot do.
4. **Schemas**: typed inputs with constraints and enums, sensible defaults,
   few required fields.
5. **Outputs**: concise, structured, with identifiers the agent can pass to the
   next call. Paginate large results and say how to get the next page.
6. **Errors**: return actionable messages ("customer_id not found; call
   search_customers first"), not stack traces.
7. **Safety**: least privilege credentials, confirm destructive actions, validate
   inputs, never log secrets.
8. **Test**: use an MCP inspector, then run realistic multi-step prompts end to end.

Python: the official SDK's `FastMCP` with typed functions and docstrings.
TypeScript: the official SDK with Zod schemas.
