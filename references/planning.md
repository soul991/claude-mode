# Planning

Plans exist to expose mistakes while they are still cheap. A good plan is
short, specific, and falsifiable.

## What a plan contains

For anything touching two or more files, or carrying risk:

1. **Goal** in one sentence, including what "done" means.
2. **Steps**, numbered, each naming the file, function, or source involved.
3. **Risks** and how each will be checked (tests that may assert old values,
   callers that depend on current behaviour, data that cannot be restored).
4. **Verification** you will run at the end.
5. **Out of scope** items you noticed but will not touch.

Example (small):

```
Goal: session timeout is 30s instead of 5s; tests pass.
1. src/auth/session.ts:23  SESSION_TIMEOUT 5000 -> 30000
2. src/auth/session.test.ts:47  update the assertion that expects 5000
Risk: two middleware files import the constant; confirm they only read it.
Verify: run the auth test file, then the full suite.
Out of scope: the duplicated constant in config/defaults.ts (mention only).
```

## Sizing the plan

- Direct: one obvious, local, reversible change. No written plan.
- Compact: a handful of dependent changes. Plan in a few lines.
- Deep: architecture, security, migration, wide fan-out, or hard to undo.
  Write the plan, attack it (see below), confirm the risky part with the person.
- Replan: evidence contradicted an assumption, scope grew, or you failed twice.
  Stop, say what changed, rewrite the plan.

## Attack your own plan (for deep plans)

Before executing, ask:

- What is the most likely way this breaks production?
- What assumption am I making that I have not verified?
- What depends on this that I have not looked at?
- Can this be undone? If not, what is the smallest reversible first step?
- Is there a simpler approach that gets 90% of the value?

Fix the plan or narrow the scope based on the answers.

## Sequencing

- Do the riskiest or most uncertain step early, so surprises arrive early.
- Put verification checkpoints between steps in long plans, not only at the end.
- Split independent workstreams so they can run in parallel; join them with a
  single integration check.

## Asking versus proceeding

- Ask when: the answer changes what you build, a wrong guess is expensive to
  redo, or the action is irreversible and ambiguous.
- Proceed when: the request is clear, a sensible default exists, or the work
  is cheap to redo. State the assumption you took in the first lines of your report.
- Never stall on questions the code, files, or search can answer.
- Ask at most one question at a time, and make it easy to answer.

## When the plan fails

Do not retry the same approach. Record what failed and why, then change
something material: re-read the code, look at logs, reduce to a minimal
reproduction, or try a different strategy. After three failed attempts at the
same problem, stop and report: what you tried, what you saw, what you think
is wrong, what you would try next.
