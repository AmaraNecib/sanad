# Engineering Workflow

Canonical lifecycle for changes in **Sanad**. The `feature-implement` skill is the
mandatory orchestrator; this document is its reference.

## Repository

- Remote: GitHub (`origin`) — `github.com/AmaraNecib/sanad`
- Base branch: `main`
- Runtime: **Bun**. Planned stack: Effect v4, Drizzle ORM, SQLite (`bun:sqlite`),
  headless Pi RPC workers, SDK-embedded Parent agent.
- Checks (to be wired once the workspace is scaffolded):

```bash
bun run lint        # lint
bun run typecheck   # types across workspaces
bun run test        # unit/integration
```

Until those scripts exist, a change states explicitly which checks were and were
not run. Never imply a check passed when it was skipped.

## Feature lifecycle

```
Ticket/spec (.scratch/issues/ or GitHub issue)
    ↓
Pin review tier + base SHA (merge-base with main)
    ↓
Design (.scratch/implementation/<issue-id>-design.md)
    ↓
Implementation (TDD)
    ↓
Guard Phase 1 — pre-commit checks
    ↓
Quality check — relevant skills
    ↓
Debate — High-assurance only
    ↓
Test audit — Standard + High-assurance
    ↓
Code review — standards + spec axes against the pinned base SHA
    ↓
Guard Phase 2 — pre-push gate
    ↓
Push + PR (user approves)
    ↓
Greptile review (when configured)
    ↓
Guard Phase 3 — pre-report gate
    ↓
Capture wisdom + report
```

Do not run a later phase without recording the earlier gate, its commands, and its
result.

## Review tiers

| Tier | Applies to | Required review |
| --- | --- | --- |
| Lightweight | Truly non-reviewable files only (`.gitignore`, `LICENSE`, `.scratch/`) | Guard Phase 1 → quality check → report |
| Standard | Code, tests, config, docs, skills | Guard 1 → quality check → test audit → code review → Guard 2 → Greptile (when configured) → Guard 3 |
| High-assurance | Recovery/decision logic, schema & migrations, launch journal, worktree lifecycle, credential handling | Standard plus debate |

High-assurance examples in Sanad: decision-log semantics, conflict closure,
recovery invariants, write-ahead intent, commit adoption, usage provenance.

## Tickets and specs

- Draft tickets live in `.scratch/issues/` (ignored) until they graduate to GitHub issues.
- Designs live in `.scratch/implementation/<issue-id>-design.md`.
- Review evidence lives in `.scratch/reviews/<issue-id>/<head-sha>-<gate>.md`.
  Evidence filenames must contain the exact reviewed HEAD SHA; any later
  reviewable change makes the evidence stale.
- Durable lessons go to `.agents/wisdom/`.

## Source-only change policy

Builds and test runs may generate `dist/`, coverage, and other ignored artifacts.
Those are never part of a source change. Before committing:

```bash
git diff --name-only <base-sha>...HEAD
git status --short --ignored
```

Stage named source/config/test/evidence files only. Never use `git add -A`.

## Merge rules

The agent never merges on its own initiative. Merge requires: explicit user
instruction, all local gates green, CI green when the branch has CI, and a clean
Greptile result when configured. Squash merges only.

## Design baseline

The Phase-1 design register (Design B decision log, recovery invariant, Q1–Q6,
G1–G6) is frozen. Changes to those invariants require explicitly reopening the
specific decision — not a side effect of an implementation PR.
