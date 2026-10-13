# Skills

Agent skills used to develop Sanad. Provenance and licenses are recorded in
[`../../skills-lock.json`](../../skills-lock.json).

## Sources

| Source | License | Skills |
|---|---|---|
| `mattpocock/skills` | MIT | ask-matt, code-review, codebase-design, diagnosing-bugs, domain-modeling, grill-me, grill-with-docs, grilling, handoff, implement, improve-codebase-architecture, prototype, research, resolving-merge-conflicts, tdd, to-spec, to-tickets, triage, wayfinder, writing-for-agents, writing-great-skills |
| `dmmulroy/anti-slop` | MIT | install-anti-slop |
| `AmaraNecib/mani-project` (local, custom) | — | feature-implement, guard, test-audit, cli-review, greploop, capture-wisdom, debate, unslop |
| `AmaraNecib/tuari_react_hono` (local, custom) | — | crew-dispatch |

The MIT-licensed skills are included with their upstream license terms; the
original repositories remain the source of truth for updates.

## How they are used

- `feature-implement` is the **mandatory orchestrator** for a change; see
  [`docs/engineering-workflow.md`](../../docs/engineering-workflow.md).
- `grilling` / `grill-with-docs` / `domain-modeling` are for design work.
- `guard`, `code-review`, `test-audit`, `greploop`, `cli-review` are the review gates.
- `tdd`, `diagnosing-bugs`, `implement`, `codebase-design`,
  `improve-codebase-architecture`, `prototype` are implementation tools.
- `crew-dispatch` is for running parallel agent lanes on separate worktrees while
  developing Sanad itself.
- `capture-wisdom` files durable lessons under `.agents/wisdom/`.

## Updating

`skills-lock.json` records the upstream source and a SHA-256 of each `SKILL.md`.
When updating a skill, update its hash in the lock in the same change.
