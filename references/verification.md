# Verification: proving the work is correct

Verification means running something that can fail and reading the result.
Re-reading your own code is not verification.

## Evidence ladder (strongest first)

1. An executable acceptance check for the exact requirement
2. Running the real program or integration end to end
3. The project's test suite
4. Compiler or type checker
5. Linter or other deterministic static analysis
6. A minimal reproducer that failed before and passes now
7. A diff review for structural invariants (no stray files, no secrets, scope respected)
8. Review by an independent reader
9. Your own re-read (supplementary only; never counts as proof)

Use the highest rung available. Say which rung you reached.

## Common commands (adapt to the project)

| Stack | Types | Lint | Tests |
|-------|-------|------|-------|
| TypeScript | `tsc --noEmit` | `eslint .` | `vitest run` / `jest` |
| Python | `mypy .` | `ruff check .` | `pytest -q` |
| Rust | `cargo check` | `cargo clippy` | `cargo test` |
| Go | `go vet ./...` | `staticcheck ./...` | `go test ./...` |
| Java | `mvn compile` | project linter | `mvn verify` |

Use what the project already uses; check package scripts and CI config first.

## Scope of checking

Start narrow, widen as confidence demands:

1. the test or check nearest the change
2. the neighbourhood (same module, direct dependents)
3. the full suite
4. build and, where relevant, a manual run

Always compare to a baseline: how many tests passed before versus after.

## Evidence required per claim

| Claim | Minimum evidence |
|-------|------------------|
| Tests pass | pass count and zero failures, from this session |
| Lint clean | linter output with no errors |
| Fixed | the failing behaviour before and the passing behaviour after |
| No regressions | before/after counts |
| Faster | measured numbers before and after |
| Rendered correctly | you opened or rasterised the output and looked |
| Numbers correct | you recomputed them with code, not by eye |

## When a check fails

1. Read the actual failure output. Do not guess.
2. Decide: is it your change, a pre-existing failure, or a flaky test?
3. Fix the cause, not the symptom. Do not weaken or delete a test to get green
   unless the test is genuinely wrong, and say so if you do.
4. Re-run the whole relevant chain, not only the failed step.
5. After three failed cycles, stop and report with the full diagnosis.

## Reporting results

End with a plain statement:

```
Result: PASS
Checked: <commands run>
Output: <the lines that matter>
Not checked: <what you could not or did not verify>
```

or the same with `FAIL`, the failing output, the suspected cause, and the fix needed.
Never report selectively. If some tests failed, say so, even when they look unrelated.
