# Server / Internet-Mail Workstream

## Purpose

Implement the hosted OceanMail service and authoritative bridge to conventional public Internet mail/services.

## Repository

`OceanMail/oceanmail-server`

## Current architecture

Server owns hosted accounts/authentication, mailbox/service state, Internet-facing service APIs/jobs, public Internet-mail ingress/egress, and server-authoritative policy/accounting/abuse/billing behavior. OceanMail-operated Server/infrastructure is the sole public SMTP/MX boundary; Internet-connected Stations/gateways do not independently deliver to arbitrary public SMTP systems. Lower-layer radio/modem/HERMES integration remains Station/upstream responsibility.

Cross-component constrained-link authentication/privacy requirements are defined in `docs/specifications/constrained-link-authentication-privacy.md`.

Cross-component Grid accounting, user approval, Station working-ledger, and Server-authoritative balance/credit/service-policy semantics are defined in `docs/specifications/grid-accounting-metering-and-service-policy.md`.

Hosted functions are logically decomposed so they can later scale independently while initially coexisting on one VPS or a small number of VPSs. Current logical service domains are:

- Internet email ↔ OMail conversion/external mail handoff;
- account/identity/authentication;
- encrypted telemetry/log ingestion, reputation/contribution analytics, abuse/AUP and network-health processing;
- Grid coordination and authoritative data publishing;
- software health/update/configuration and regional/Grid dataset distribution;
- internal administrative/control-plane tooling.

See `docs/architecture/backend-service-decomposition.md`.

Native OMail transport, relay/store-and-forward execution, durable local transfer state, and disconnected routing/peer intelligence remain Station-owned. The hosted backend must not become a mandatory real-time transport engine for native boat-to-boat OMail. Server is required when traffic crosses between native OMail and conventional public Internet mail/services or when another centrally managed service explicitly requires it.

## Current implementation state

The active 0.2 Server repository is a public documentation/bootstrap repository.
Production authentication, MFA, queues and persistence require implementation and
validation against current contracts.

The preliminary low-bandwidth News direction is preserved in `docs/specifications/news-feed.md`: bounded curated RSS/Atom ingestion, Server-side text-first normalization/provenance/source policy, and future Grid caching only after rights/object/cache/scheduling questions are settled. It is not implementation-ready and does not authorize global feed mirroring or speculative mesh replication.

## Major outstanding work

- define the narrow authenticated Station/Server and direct-client/Server service contracts;
- settle production account/identity/authentication boundaries with Station production authentication work work;
- define device credential/revocation, constrained-link replay resistance, and recoverable/idempotent destructive-mailbox semantics without transmitting reusable mailbox secrets over shared radio links;
- implement hosted mailbox/account/service foundations;
- implement centralized public SMTP/MX ingress/egress with durable queueing, destination retry, bounce handling, DKIM/SPF/DMARC alignment, reputation, and abuse/rate controls;
- define truthful evidence mapping across OMail gateway acceptance, Server acceptance, public SMTP delivery, and later receipts where available;
- define structured encrypted Station telemetry ingestion/acknowledgement/retention contracts;
- implement server-authoritative accounting/abuse/billing/reconciliation policy;
- define Grid dataset/reputation publication and software/config distribution contracts without creating central runtime dependence for native OMail;
- for News, settle source rights, article/object/manifest semantics, caching, accounting/scheduling, and the first narrow Server/Station contract before implementation;
- coordinate with Infrastructure on provider/hosting, IP/reputation, HA/recovery, deployment security, backup requirements, and later service separation.

## Constraints

- Gateway Stations are OceanMail transport participants, not public Internet MTAs.
- A temporary Server outage may delay Internet-boundary traffic but must not disable native OMail paths.
- Exact provider, host count, geographic placement, IP allocation, and scale-out topology remain deployment decisions; do not infer them from historical prototypes.
- Logical service separation does not require one VPS per service in the initial deployment.
- Do not distribute public-SMTP relay credentials or public-MTA responsibilities to Stations merely because they already run local SMTP/Postfix.

## Urgent shared-data designation

[ADR-008](../docs/decisions/ADR-008-four-band-scheduling-and-channel-use.md) gives Server authority to promote normally Band 3 shared updates (for example security updates or piracy notices) into Band 1. Designations require authenticated origin, scope, and freshness. They do not become Band 0 Emergency or qualify for full-lease route establishment; Station applies its normal Band 1 cap and capacity/authorization policy.

The designation/distribution contract is outstanding implementation work. Station continues to own channel selection, relay execution, shared broadcasts, and offline scheduling; this does not make native routing depend on a live Server.

## Accepted personal-traffic boundary (2026-09-22)

Band 1 is public discovery/route/access coordination plus authorized urgent public updates. Band 2 includes ordinary manifests, requests, receipts, custody/repair/stop-flow/tombstones, account reconciliation, and payload, with expedited mail control within its fairness shares. Bands 0/1/3 are public over HF. Client–own Station, direct Client–Server Internet, and gateway–Server connections are always authenticated and encrypted. Personal HF encryption, if adopted, terminates at Station and Server through untrusted relays/gateways; the deployed path has no plaintext capability or fallback. A single deployment choice remains pending feasibility, not a user or per-message option. External SMTP is a separate boundary without a universal encryption guarantee.

[ADR-009](../docs/decisions/ADR-009-personal-traffic-and-encryption.md) governs follow-on work. Component classification, API/transport security, and key management require implementation and validation; no production capability is claimed by this documentation.
