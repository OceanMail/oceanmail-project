# Architecture Decision Records

Major organization-level architectural decisions live here. Smaller decisions belong in root `DECISIONS.md`.

Current ADRs:

- [`ADR-001-project-documentation-authority.md`](ADR-001-project-documentation-authority.md) — central project spine and authority boundary.
- [`ADR-002-hermes-mercury-upstream-first.md`](ADR-002-hermes-mercury-upstream-first.md) — HERMES/Mercury upstream-first communications foundation.
- [`ADR-003-client-station-server-boundaries.md`](ADR-003-client-station-server-boundaries.md) — Client/Station/Server/Infrastructure separation and external-mail boundary ownership.
- [`ADR-004-station-store-transport-grid-control.md`](ADR-004-station-store-transport-grid-control.md) — Station STORE/TRANSPORT versus GRID/CONTROL separation, including relay/gateway/OChat placement and superseded Priority-era details.
- [`ADR-005-delivery-evidence-and-repair.md`](ADR-005-delivery-evidence-and-repair.md) — authoritative delivery evidence, stable logical message identity, patient query-before-retry behavior, bounded reinjection, and future bounded relay-copy semantics.
- [`ADR-006-centralized-public-internet-mail-boundary.md`](ADR-006-centralized-public-internet-mail-boundary.md) — centralized public SMTP/MX authority while preserving decentralized native OMail.
- [`ADR-007-hf-link-capacity-tiers-and-survival-mode.md`](ADR-007-hf-link-capacity-tiers-and-survival-mode.md) — progressive HF capacity tiers, survival-mode suppression, and bounded high-value relay eligibility.
- [`ADR-008-four-band-scheduling-and-channel-use.md`](ADR-008-four-band-scheduling-and-channel-use.md) — Bands 0–3, capped control/route-establishment exception, remaining-time ordinary payload, unreserved shared broadcasts, Server promotion, and single-radio channel behavior.

- [`ADR-009-personal-traffic-and-encryption.md`](ADR-009-personal-traffic-and-encryption.md) — ordinary mail metadata/control in Band 2, public Bands 0/1/3, and Station-to-Server encryption boundaries with one pending deployment choice and no plaintext path if encryption is adopted.

Historical accepted decisions currently preserved under `oceanmail-desktop/docs/decisions/` remain rationale sources until individually migrated or indexed here. Where they conflict with ADR-001 on documentation authority, ADR-001 supersedes that authority claim while preserving the underlying product decision unless separately superseded.
