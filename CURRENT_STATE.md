# OceanMail Current State


Updated: 2026-09-26

This is a snapshot of current organization-level truth, not a chronological diary.

## Active 0.2 repositories

- `OceanMail/oceanmail-project` — organization-level documentation spine and durable project memory.
- `OceanMail/oceanmail-desktop` — active Thunderbird-based Desktop implementation and client-specific product/design material.
- `OceanMail/oceanmail-station` — active headless Station implementation and HERMES/Mercury laboratory integration.
- `OceanMail/oceanmail-server` — active 0.2 hosted-service boundary, currently early/bootstrap rather than a completed service.
- `OceanMail/oceanmail-infrastructure` — active 0.2 deployment/operations boundary, currently early/bootstrap.

All four active component repositories point organization-level architecture/governance work to this project spine while retaining implementation-specific documentation locally.

The dedicated `OceanMail` GitHub organization is the canonical repository home. The active Desktop repository is intentionally named `oceanmail-desktop` rather than generic `oceanmail`.

## GitHub Actions / CI execution boundary

All five public repositories use GitHub-hosted checks and protected `main`.
Public PRs must not use trusted self-hosted runners or maintainer workstations.
Operational inventories stay outside source. See the
[public CI policy](https://github.com/OceanMail/oceanmail-infrastructure/blob/main/docs/CI-RUNNERS.md).
External-fork acceptance remains unverified.

## Communications architecture

OceanMail 0.2 is HERMES/Mercury upstream-first. BEMPIC is frozen and M4P integration is tabled; neither is on the active 0.2 critical path.

Station has proven the no-radio store/transport path through Phase 4I, including SMTP/Postfix, HERMES `uuxcomp`, Taylor UUCP, Mercury simulated constrained transport, remote mailbox evidence, and a returned receipt correlated back to the original message/job. Accepted trust remains laboratory-only (`lab_peer_transport_unverified`), not production cryptographic peer authentication or human-read proof.

Phase 4I also identified a reciprocal-session stale-data defect in the pinned HERMES VARA/Mercury bridge. OceanMail carries a narrow tracked laboratory patch; current `Rhizomatica/hermes-net/main` was rechecked on 2026-09-11 and still lacks that fix. Upstream resolution remains outstanding; the local patch/lifecycle gates must remain until an upstream replacement is accepted and the reciprocal acceptance is rerun.

Native OMail remains decentralized: boat-to-boat/store-carry-forward OMail must not require Internet access or central Server availability. When traffic crosses between OMail and conventional public Internet mail, OceanMail-operated Server/infrastructure is the sole public SMTP/MX boundary. Internet-connected Stations/gateways do not become independent public MTAs or deliver directly to arbitrary Internet SMTP systems. See ADR-006.

Physical-radio Phase 5 remains deferred pending explicit authorization and suitable hardware/test scope. The exact FCC pathway for resolving the contemplated OceanMail HF test/deployment model remains unresolved; see `workstreams/regulatory-compliance.md`.

Future real-radio scheduler/rendezvous work must remain functional with one HF transceiver; simultaneous multi-radio operation is an optimization rather than a baseline dependency. This retained constraint is research-scoped and does not authorize Phase 5.


HF scheduler policy in ADR-007 uses an initial delivered-throughput design range
of approximately 0.1–3 kbps and progressive capacity tiers. Below 0.1 kbps,
survival mode suppresses deferrable/bulk work while retaining bounded high-value
relay opportunities. Emergency remains subject to technical capability and
legal/operational permission; neither tier nor label authorizes transmission.
This is design policy, not implemented scheduler or field-test evidence.

## Station current work

The in-memory lease controller is supplemented by public
[Station PR #1](https://github.com/OceanMail/oceanmail-station/pull/1), merged on
2026-09-26: traffic classification, route-attempt backoff, Band 2 selection and a
deterministic no-radio harness, plus auth regression tests. These modules are
experimental and not connected to daemon transport dispatch. Restart-durable
accounting, capacity-tier integration, channel coordination and live validation
remain outstanding. See
[LEASE_CONTROLLER.md](https://github.com/OceanMail/oceanmail-station/blob/main/docs/LEASE_CONTROLLER.md).

Laboratory authentication/context endpoints are implemented; see the public
[Phase 4J contract](https://github.com/OceanMail/oceanmail-station/blob/main/docs/PHASE4J_AUTH_FOUNDATION.md).
Production identity/enrollment, LAN exposure, private persistence, real Available,
accounting and physical radio remain separate gates. The
[Station/client implementation gates](docs/specifications/station-client-implementation-gates.md)
record these boundaries. No fixture or lab credential is production private state.

Follow-on work includes production account/user/device authorization, real
Available/retrieval/accounting APIs, HERMES lifecycle fixes, production storage
encryption/key separation, Grid/control and relay/gateway execution.

## Desktop current work

OceanMail Desktop is a dedicated OceanMail application built on a pinned Thunderbird foundation plus mandatory OceanMail extension/behavior. Stock Thunderbird coexistence is required.

Current Desktop truth includes:

- native Thunderbird shell rather than a second primary navigation rail;
- account-scoped `Available` as remote/private manifest state rather than an IMAP folder;
- account Mail hierarchy `Inbox / Available / Saved / Drafts / Sent / Trash` and no user-facing OceanMail Outbox;
- no user-facing ordinary transport Priority class;
- Emergency as the only user-originated transport-precedence class;
- `Important` as interoperable message metadata only;
- fixture/demo state must remain visibly distinct from real Station evidence;
- OChat is live/ephemeral, not ordinary store-and-forward, and pending text is not presented as sent until authoritative transmission evidence exists.

The Desktop alpha baseline includes native mail integration and account-scoped views. Current behavior and evidence are documented in the [Desktop documentation index](https://github.com/OceanMail/oceanmail-desktop/blob/main/docs/README.md). Accepted design documents do not imply implemented Station APIs or live Grid evidence.

Major implementation dependencies remain real authenticated Station APIs/account grants, authoritative Available/accounting operations, trustworthy per-message Sent evidence, packaging/update readiness, and later real OChat/Station contracts.

## Grid accounting and service policy

The cross-component Grid accounting relationship is now durably specified:

- ordinary constrained-link payload retrieval requires recipient selection/approval regardless of small message size;
- sender pays the applicable ordinary constrained send quota;
- recipient pays applicable ordinary receive quota for selected/approved content successfully received;
- third-party relay/gateway work does not debit a local user's ordinary send/receive Grid quota, but remains metered and locally resource-controlled;
- Station may maintain disconnected working ledgers and contribution evidence but cannot mint globally authoritative credit;
- Server remains authoritative for global balances, reconciliation, contribution-credit qualification, billing/service policy, and mutable quota/credit thresholds.

Numeric quota/price/credit/resource thresholds are service policy rather than fixed protocol architecture unless a conceptual relationship changes.

## Server and Infrastructure

The active Server and Infrastructure repositories define their 0.2 component boundaries and include concise project-spine-aware `AGENTS.md` files. Their implementation remains early/bootstrap.

Both repositories document the centralized public SMTP/MX boundary and current component responsibilities.

The architectural public-mail boundary is settled: OceanMail-operated Server/infrastructure is the only public Internet SMTP/MX authority. Remaining deployment work includes provider/hosting choice, host count/geography, IP/reputation operations, HA/recovery, and the authenticated Station/Server gateway contract. A central outage may delay Internet-boundary traffic, but native OMail must continue independently.

Production MFA requires implementation and validation against the current Server identity/account contracts.

## News / bounded low-bandwidth content

A preliminary News direction is preserved but is not implementation-ready. Initial Internet-side acquisition is bounded/curated, with RSS/Atom preferred where selected sources provide it and Server-side text-first normalization/provenance/source policy. Any future Grid caching must respect current STORE/TRANSPORT versus GRID/CONTROL boundaries and may not be used to justify speculative global mesh behavior. Source rights, object/manifest design, cache policy, scheduling/accounting, and measured compression/throughput remain unresolved before implementation.

## Publication/readiness state

All five repositories are public with installed AGPL-3.0-only code and
CC-BY-SA-4.0 documentation licenses. Contributors can fork and submit PRs;
maintainers review and merge. No additional inbound agreement is adopted.
See [PUBLICATION.md](PUBLICATION.md), [CONTRIBUTING.md](CONTRIBUTING.md) and
the [release checklist](docs/specifications/publication-readiness.md).
Source publication is separate from production, binary and RF readiness.

## Documentation-spine state

Project owns organization-wide architecture, decisions, terminology and workstreams.
Component repositories own their implementation details and public evidence.
Current documentation must be self-contained; older technical summaries must be
labeled as historical and must not serve as current CI or open-PR status.
Follow [chat reconciliation](docs/specifications/chat-reconciliation.md) when
preserving durable decisions; new summaries do not make older evidence current.

## Intentionally deferred

- physical-radio Phase 5 until explicitly authorized;
- mobile implementation until Desktop matures;
- speculative multi-hop routing/mesh implementation pending measured need;
- BEMPIC resumption absent comparative evidence;
- M4P integration absent demonstrated need;
- production-scale infrastructure/clustering before measured requirements justify it;
- broad News/feed crawling or redistribution before source-rights/object/cache policy is settled.

## Major unresolved organization-level questions

- exact production identity/enrollment/authentication model across Server, Station, account, user, and device;
- production cryptographic trust for returned receipts and holder-side Available disclosure;
- production storage/key-separation architecture;
- public Internet-mail provider/hosting, host-count/geographic, IP/reputation, HA, and recovery details within the centralized Server boundary;
- implementation and field validation of relay/gateway policy and the Station/Server gateway contract;
- FCC regulatory path and authoritative clearance for the exact OceanMail HF test/deployment model, including licensing/equipment-authorization implications;
- exact Grid quota/credit/pricing/resource-policy values and policy-distribution security details;
- News source rights/object/cache/scheduling implementation details;
- licensing/publication decisions for currently private 0.2 repositories.

## Scheduling design update (2026-09-21)

[ADR-008](docs/decisions/ADR-008-four-band-scheduling-and-channel-use.md) defines Bands 0–3: Emergency and its own control; public network coordination plus Server-promoted urgent public updates; ordinary local/relay mail metadata, control and payload; shared background broadcast data. Lease duration and normal Band 1 cap are independent tuning inputs, with a full-lease necessary route-establishment exception. Ten/four minutes are arithmetic examples, not selected defaults or a fixed 40% ratio. Band 2 uses remaining time. Band 3 has no reserved lease share and uses idle or announced broadcast opportunities.

Rendezvous announcements lead to negotiated directed exchanges (Band 1 then Band 2 on the same channel) or shared time/channel-announced broadcasts. Single-radio listening and Emergency discovery/preemption must be bounded and validated. User/ship byte budgets, Station airtime budgets, local/relay fairness, and bounded relay acceptance remain required. This supersedes the six-band/reserved-slot drafts; implementation and runtime validation remain outstanding. Tracking is inconsistent: Station issue #22 is closed as of 2026-09-22, while the component PR #50 and current project records state that its first slice does not close the remaining work. A follow-up tracker is needed; the full ADR implementation is not complete.

## Configurable lease controller (2026-09-22)

The first in-memory lease controller is supplemented by public
[Station PR #1](https://github.com/OceanMail/oceanmail-station/pull/1), merged on
2026-09-26: traffic classification, route-attempt backoff, Band 2 selection and a
deterministic no-radio harness, plus auth regression tests. These modules are
experimental and not connected to daemon transport dispatch. Restart-durable
accounting, capacity-tier integration, channel coordination and live validation
remain outstanding. Lease duration and control allowance are independent inputs;
ten/four minutes are examples, not defaults. See
[LEASE_CONTROLLER.md](https://github.com/OceanMail/oceanmail-station/blob/main/docs/LEASE_CONTROLLER.md).

## Personal traffic and encryption decision (2026-09-22)

Band 1 is public discovery/route/access coordination plus authorized urgent public updates. Band 2 includes ordinary manifests, requests, receipts, custody/repair/stop-flow/tombstones, account reconciliation, and payload, with expedited mail control within its fairness shares. Bands 0/1/3 are public over HF. Client–own Station, direct Client–Server Internet, and gateway–Server connections are always authenticated and encrypted. Personal HF encryption, if adopted, terminates at Station and Server through untrusted relays/gateways; the deployed path has no plaintext capability or fallback. A single deployment choice remains pending feasibility, not a user or per-message option. External SMTP is a separate boundary without a universal encryption guarantee.

See [ADR-009](docs/decisions/ADR-009-personal-traffic-and-encryption.md). This records accepted design, not deployed encryption or traffic-classification evidence. Existing runtime/RF and production-security gates remain in force.

## CI retrofit coordination

G0 registers the [rollout and measurement tracker](docs/specifications/ci-quality-retrofit.md). Station S1 is first: report-only tooling and exact-head evidence. No baseline, required quality gate or branch enforcement is established by this governance work. Work beyond S1 awaits separate owner direction.


## Public implementation updates — 2026-09-26

- [Desktop PR #1](https://github.com/OceanMail/oceanmail-desktop/pull/1) adds stale-render guards for Dashboard/Watch; live Thunderbird acceptance remains outstanding.
- [Desktop PR #2](https://github.com/OceanMail/oceanmail-desktop/pull/2) repairs the Station auth integration runner and its provenance reporting.
- [Infrastructure PR #1](https://github.com/OceanMail/oceanmail-infrastructure/pull/1) adds a public-source verification utility. Its checks do not certify production readiness or all administrative settings.

These public changes supersede older implementation snapshots only in their stated scope.
