# OceanMail Organization — Agent and Contributor Instructions

## Authority

Git is authoritative. Chat history, agent memory, PR descriptions, issue text, and handoffs are useful context but do not silently override accepted repository documentation.

The human owner is final authority for product direction, major architecture, security/privacy, merge/release, regulatory, and safety-sensitive decisions.

Current operating roles:

- **Claude** — primary programmer since 2026-10-27; plans and carries out bounded work within the settled architecture: code development, maintenance, troubleshooting, tests, CI repair, documentation upkeep, commits and PRs. Has architectural latitude: proposes needed architecture changes to the owner, and the owner and Claude may decide them without ChatGPT. Does not merge and does not count its own review as independent evidence.
- **ChatGPT** — optional big-picture architecture/decision role when the owner wants it, and independent bug-finding review of Claude's work when the owner asks. Not a day-to-day planner.
- **Codex** — no standing role since 2026-10-27; it was previously the primary implementation agent.
- **Git/GitHub** — durable source of project truth and implementation evidence.

The detailed operating workflow is defined in [`docs/specifications/ai-development-workflow.md`](docs/specifications/ai-development-workflow.md).

## Required reading before substantial work

1. `PROJECT.md`
2. `CURRENT_STATE.md`
3. `DECISIONS.md`
4. `REPOSITORIES.md`
5. `docs/specifications/ai-development-workflow.md` when planning, implementing, or reviewing AI-assisted development work
6. the relevant `workstreams/*.md`
7. relevant ADR/specification/interface documents in this repository
8. the owning component repository's `AGENTS.md`, current status/docs, source, open PRs/issues, and tests as applicable

Do not reconstruct OceanMail architecture from old AI assumptions when Git contains newer truth.

OceanMail's purpose, plan and mission are foundational. Change accepted architecture only when needed (especially for law/regulation or verified technical limits), through the escalation gate below. Claude may raise such changes; the owner decides, with or without ChatGPT.

## Conflict handling

If documentation conflicts with implementation, another document, an issue, or a PR:

1. identify the conflict explicitly;
2. determine which source is current and authoritative;
3. preserve history/supersession rather than rewriting it invisibly;
4. update the owning documents so the next contributor does not rediscover the conflict.

Never silently choose the version that makes implementation easiest.

## Architecture escalation

If accepted architecture is technically impossible, materially unsafe, incompatible with verified upstream behavior, or requires a major redesign, stop architectural improvisation and report:

```text
BLOCKED / ARCHITECTURAL DECISION REQUIRED

Observed:
Why current design is problematic:
Evidence:
Options:
Recommended option:
Affected repositories/files:
```

Record the resulting decision in Git before implementation proceeds.

## Repository ownership rule

Organization-wide truth belongs here. Component implementation truth belongs in the component repository. Do not duplicate large implementation documents into `oceanmail-project`; link to them.

When component behavior changes organization-level architecture, terminology, cross-component contracts, or settled semantics, update both the component-local documentation and the appropriate project-spine document.

## Truthfulness and evidence

Separate verification into:

- **STATIC / UNIT** — lint, unit tests, static/build checks.
- **INTEGRATION** — service/protocol interaction, Docker labs, CI.
- **LIVE / PRODUCT** — actual UI, live Station, real RF/hardware, field behavior.

Never claim stronger evidence than was observed. In particular, local queue state, transfer progress, remote mailbox receipt, returned receipt, and human reading are distinct claims.

## Security/privacy baseline

- Fail closed when authorization, trust, accounting permission, or evidence is unknown where appropriate.
- Device trust is not user authorization.
- Station/Captain/Admin authority does not inherently grant another user's mailbox/private Available access.
- Do not expose the Station LAN API without accepted authentication/authorization.
- Do not treat laboratory plaintext storage as production security readiness.
- Do not commit secrets, private keys, credentials, tokens, customer data, or sensitive production material.

## Upstream discipline

HERMES/Mercury work is upstream-first. Preserve exact pins where component docs require them. Keep necessary downstream integration deltas explicit, narrow, auditable, provenance-tracked, and license-preserving. Do not silently copy/fork lower-layer implementations into OceanMail code.

## Before finishing substantial work

Update, as applicable:

- component implementation/status docs;
- `CURRENT_STATE.md` if organization-level state materially changed;
- `DECISIONS.md` for newly settled semantics/behavior;
- an ADR/specification/interface document for major architecture changes;
- the relevant workstream document;
- the active scoped handoff, if one exists.

Temporary handoffs must never become the only location of permanent knowledge.

## Chat/conversation reconciliation

When retiring an AI conversation, follow `docs/specifications/chat-reconciliation.md`. Extract only durable decisions, unresolved questions, evidence, active state, and rationale that are missing from Git. Do not dump raw chat transcripts into the spine.

For retired or old conversations, temporal precedence is mandatory: the new timestamp of a reconciliation commit never makes the underlying old chat decision new. Current Git/merged implementation evidence wins unless the thread contains a clearly later owner decision, and uncertain legacy material must remain historical/research/candidate/unresolved rather than being promoted to ACTIVE/CURRENT.

## Merge/workflow discipline

Respect the owning repository's current `AGENTS.md` and workflow. Preserve unrelated work. Do not force-push/reset others' work. Cross-repository contract changes must be reconciled at the project level rather than implemented independently on each side.

For normal OceanMail repository work, use a topic branch and pull request rather than committing substantive changes directly to `main`. The default integration method is a **merge commit**, preserving branch/PR history and review/evidence lineage. Use squash or rebase merge only when the owner explicitly directs it for that change.

Active non-default branches must have a visible purpose. After a pull request is merged or otherwise superseded, verify that the source branch contains no unique work that still needs preservation, then delete/retire it rather than allowing stale branches to accumulate as ambiguous pseudo-authority. Periodically classify aging branches as active, merged, superseded, or intentionally historical before relying on them. This branch-hygiene rule does not authorize automatic merging; merge authority remains governed separately.

## CI retrofit assignments

For retrofit work, read [the rollout specification](docs/specifications/ci-quality-retrofit.md), the assigned task, and component instructions. Every retrofit PR requires an independent review of the exact proposed head by a reviewer other than the authoring session (a separate fresh-context Claude review session, or ChatGPT at the owner's request), including small tooling/documentation PRs; this scoped rule supersedes the general optional-review default. Claude proposes a disposition for each finding, the owner decides disputed or architectural ones, and the owner controls merge/protection. Keep measurement, mechanical cleanup, adapters, baseline seed, CI, characterization, audits and fixes in separate PRs. Unknown metrics are not zero. Do not advance beyond the assigned phase. This repository has no CLAUDE.md convention; these shared instructions apply to Claude too.
