# Development Workflow

Permanent development workflow for Sanad: branching, issue tracking, and planning.

## 1. Planning flow

```
Design register (frozen Phase-1 baseline)
    ↓
Architecture / ADRs (docs/adr/)  — when a decision is reopened or added
    ↓
.scratch/issues (draft planning)
    ↓
GitHub Issues (execution)
    ↓
Implementation
```

| Stage | Location | Purpose |
|-------|----------|---------|
| Design baseline | frozen register (thread/issue) | Locked invariants; changes require explicitly reopening a decision |
| Architecture | `docs/`, `docs/adr/` | Approved decisions |
| Draft planning | `.scratch/issues/` | Temporary workspace before GitHub |
| Execution | GitHub Issues | Source of truth during implementation |

## 2. Issue taxonomy

### Priority

| Label | Meaning |
|-------|---------|
| `priority:high` | Blocking for the current milestone |
| `priority:medium` | Important for the current milestone |
| `priority:low` | Deferred if time runs short |

### Area

| Label | Scope |
|-------|-------|
| `area:persistence` | Schema, migrations, decisions, conflicts, checks |
| `area:recovery` | Launch journal, reconciliation, adoption, retry |
| `area:harness` | Pi RPC worker, session identity, usage capture |
| `area:parent` | SDK-embedded Parent, brief reconstruction, wake delivery |
| `area:outbox` | Event durability, claims, idempotent application |
| `area:cli` | status/logs/sessions |
| `area:authority` | Action→policy map, approvals, abandonment |
| `area:testing` | Unit/integration/recovery tests |
| `area:tooling` | Build, lint, CI, repo scripts, dependencies |

### Type

| Label | Meaning |
|-------|---------|
| `type:feat` | New capability |
| `type:fix` | Bug fix |
| `type:refactor` | Behavior-preserving restructure |
| `type:test` | Test-only change |
| `type:docs` | Documentation only |
| `type:chore` | Tooling, deps, config |

## 3. Definition of Done

A ticket is done when:

1. All gates in `engineering-workflow.md` pass for its review tier.
2. Recovery-relevant behavior has a test that exercises the crash/restart path.
3. No generated artifacts entered the diff.
4. PR is open (or updated) with review evidence linked; merge is a separate user decision.

## 4. Milestones

Milestones follow the Phase-1 work order:

```
Step 1 schema + migrations
Step 2 write-ahead intent + outbox + idempotent drain
Step 3 worker runner (RPC, session id, terminal event, usage)
Step 4 recovery loop (launch journal, adoption, retry)
Step 5 Parent host (reattach, brief, decision)
Step 6 CLI
Step 7 unattended Windows acceptance run
```

A milestone closes only when its exit gate passes.

## 5. Phase-1 scope reminder

In scope: one repo, one task, one local worker, Windows, SQLite, outbox, recovery,
read-only CLI. Out of scope: PR creation, CI polling, external review, Docker, VPS,
Cloudflare, DAG scheduling, dashboards, multi-account, missions on the critical path.
