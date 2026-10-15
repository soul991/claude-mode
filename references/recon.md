# Recon: grounding yourself before you touch anything

Goal: learn the real state of the system in as few round-trips as possible.

## Standard first batch (run these together, not one by one)

For a code change:

- the target file
- its test file
- every reference to the symbol or constant you will change (search, do not guess)
- recent history of the file (`git log --oneline -5 -- <file>`)
- the build/lint/type config (tsconfig, pyproject, package.json, Makefile)

For a data task:

- the file's size, format, and first rows
- column names, types, null counts, obvious outliers
- any README or schema that describes it

For a bug:

- the exact error text and where it is raised
- how to reproduce it (a command that fails)
- the last change that touched that area

## Rules

- Read the file before editing. Read its imports and callers when the change
  could ripple outward.
- Confirm paths exist before using them. Search; do not guess.
- Prefer a targeted read (a function, a line range) over dumping huge files.
- In large unfamiliar repos, map first: directory layout, entry points,
  where tests live, how the project is built and run. Then go deep on the
  part that matters.
- Look for existing conventions (naming, error handling, test style) and follow
  them instead of introducing your own.

## What to write down after recon

A few lines, no more:

- the files that matter and why
- the commands that build, test, and lint this project
- any trap you found (generated files, vendored code, flaky tests, env vars)
- what is still unknown

## Stop conditions

Recon is done when you can state, in two or three sentences, what will change,
what could break, and how you will prove it worked. If you cannot, read more.
If reading more is not helping, reduce the problem to a minimal reproduction.
