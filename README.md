# Sanad

**Sanad** (سَنَد) — support, backing; an auditable chain of attribution.

Persistent, crash-recoverable orchestration for AI coding agents. Sanad coordinates
coding-agent workers, keeps authoritative state in SQLite, and continues work while
your own machine is off.

## What it is

- An orchestration layer over existing coding agents (Pi first) — not a new agent.
- A durable Task → Assignment → Attempt model with an append-only decision log.
- Event-driven: headless workers, durable completion records, deterministic recovery.
- Self-hosted; execution providers are swappable at the edges (local first, remote later).

## What it is not

- Not a coding model and not a replacement for Pi.
- Not a CI system, and not dashboard-first.
- Phase 1 does not create pull requests, poll CI, or merge.

## Status

Design validation is complete. Implementation has not started.
The Phase-1 baseline (schema, recovery protocol, acceptance gates) is frozen.

## Planned stack

Bun · Effect v4 · Drizzle ORM · SQLite (`bun:sqlite`) · headless Pi RPC workers ·
SDK-embedded Parent agent.

## Phase 1 (planned)

One repository, one task, one local worker: task → isolated worktree → repository
checks → committed branch → durable completion and usage record → Parent report.
Crash-safe and restart-recoverable. No PR, CI, review, or merge.
