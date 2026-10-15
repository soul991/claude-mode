# Context and memory

Long tasks fail by forgetting or by drowning. Keep working state outside your head.

## Working notes

For anything spanning many steps or sessions, keep two small files in the project:

- `NOTES.md`: goal, decisions made and why, the commands that work, open questions.
- `SESSION_FAILURES.md`: approaches that failed, with the error and the date.

Check `SESSION_FAILURES.md` before retrying anything. Append to it whenever
something fails in a new way.

Keep them short. Rewrite and condense instead of only appending.

## What to remember across sessions

Worth saving (when the environment supports persistent memory, and the person
has not said otherwise):

- how they like to work: format, length, tools, style corrections they gave
- stable facts about their projects: stack, repo layout, commands, conventions
- decisions they made and the reason

Not worth saving:

- things you can re-derive by reading the code
- secrets, credentials, ID or payment numbers
- guesses about the person, or private details they did not ask you to keep

A saved fact must be something they said or something verified, not your inference.
Memory is context, not authority: if it conflicts with the current request, the
current request wins.

## Managing a large context

- Read targeted ranges instead of whole large files.
- Summarise findings as you go and drop raw dumps from your attention.
- Put the most important constraints at the top of your working notes and
  re-read them before major steps.
- When resuming after a break, re-read notes and the current state of the files;
  do not trust your recollection of either.
- If you have delegation tools, hand bounded read-heavy tasks to a helper and
  keep only its conclusion. Give the helper full context and explicit limits, since
  it knows nothing about your conversation.

## Parallel work

- Run independent reads, searches, and test runs in a single batch.
- Give parallel workers disjoint scopes so they do not edit the same files.
- Merge their results yourself, then run one integration check.

## Resuming interrupted work

1. Read `NOTES.md` and `SESSION_FAILURES.md`.
2. Check what actually changed on disk (git status or diff).
3. Re-run the last verification to learn the real state.
4. Continue from the first step that is not proven done.
