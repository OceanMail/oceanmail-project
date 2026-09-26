# ADR-001 — Organization-Level Project Documentation Authority

- Status: ACCEPTED
- Date: 2026-09-11
- Supersedes: the authority portion of `oceanmail-desktop/docs/decisions/0001-documentation-and-repository-authority.md`

## Context

OceanMail accumulated architecture and implementation knowledge across multiple repositories and AI conversations. Desktop documentation became the de facto program authority, which coupled organization-level truth to one product component and made AI continuity dependent on long-running conversation context.

## Decision

`OceanMail/oceanmail-project` is the authoritative organization-level project/documentation repository.

It owns:

- overall OceanMail definition and current system architecture;
- shared terminology and stable principles;
- repository inventory and relationships;
- cross-repository interfaces and major decisions;
- current organization-level state/workstreams;
- contributor/AI operating instructions;
- historical architecture rationale and active scoped handoffs.

Component repositories own source code, component-specific tests/build/deployment instructions, internal APIs, and implementation-specific decisions.

Do not duplicate large component documentation into the project repository; link to the authoritative component source.

## Consequences

- `oceanmail-desktop/docs` no longer owns organization-level authority, although valid client/product decisions remain valid unless superseded.
- active component `AGENTS.md` files should point agents to this project spine before architecture-changing work.
- cross-repository decisions made in future work must converge here.
- old chats may be deleted after reconciliation because Git holds durable state.

## Negative decision

There will not be one mutable organization-wide `HANDOFF.md`. Handoffs are workstream-scoped and temporary.