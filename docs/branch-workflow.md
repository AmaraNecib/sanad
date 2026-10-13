# Branch Workflow

## Naming convention

- `feat/<issue-id>-<short-description>`: one feature or ticket per branch, off `main`
- `fix/<issue-id>-<description>`: repair branch
- `refactor/<issue-id>-<description>`: behavior-preserving restructure
- `agent/<description>`: isolated implementation branch for agent-driven work
- `integration/<description>`: merge-and-verify branch combining several agent branches

The issue id is the GitHub issue number (or the local `.scratch/issues/` file number
before it graduates to GitHub).

## Expectations

- Every branch targets `main` as its base.
- A feature branch states its goal, changed files, validation run, and follow-ups
  in the PR description.
- Integration branches list merged inputs, conflict-resolution notes, and the
  final verification pass.
- If a branch cannot complete validation, the PR states the gap explicitly
  instead of implying success.
- Squash merges only; never merge without an explicit user instruction.

## Worker branches (product, not development)

Sanad's own worker attempts use a separate namespace:

```
orch/<task>/<assignment>/a<seq>
```

These are created per Attempt at the recorded `base_sha`, are never reused, and
are never deleted while they contain commits. Do not confuse them with
development branches above.
