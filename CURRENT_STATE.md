# OceanMail Current State

> Publication scope update — 2026-09-26: the owner approved fresh public repositories for **all five active components: Project, Station, Desktop, Server and Infrastructure**. Preserve the original repositories privately with `-archive` suffixes. The five older BEMPIC/0.1 repositories remain private and frozen. Earlier three-repository scope statements below are superseded historical records.


> Current publication decision (2026-09-26): create fresh sanitized Project, Station and Desktop repositories with installed licenses. Preserve the original repositories privately under names ending in `-archive`. See [PUBLICATION.md](PUBLICATION.md). Earlier in-place conversion instructions and pending-license statements below are historical.


Updated: 2026-09-25

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

Desktop PR #27 and Station PR #60 moved public validation to GitHub-hosted
Ubuntu 24.04. Project, Server and Infrastructure also have hosted documentation
checks. Required settings and trusted-runner exclusion remain unverified.

Private host inventories and operational procedures are excluded from public
documentation. See `OceanMail/oceanmail-infrastructure/docs/CI-RUNNERS.md` for
the public security policy. Historical logs, artifacts and Git metadata remain
separate publication gates.

## Communications architecture

OceanMail 0.2 is HERMES/Mercury upstream-first. BEMPIC is frozen and M4P integration is tabled; neither is on the active 0.2 critical path.

Station has proven the no-radio store/transport path through Phase 4I, including SMTP/Postfix, HERMES `uuxcomp`, Taylor UUCP, Mercury simulated constrained transport, remote mailbox evidence, and a returned receipt correlated back to the original message/job. Accepted trust remains laboratory-only (`lab_peer_transport_unverified`), not production cryptographic peer authentication or human-read proof.

Phase 4I also identified a reciprocal-session stale-data defect in the pinned HERMES VARA/Mercury bridge. OceanMail carries a narrow tracked laboratory patch; current `Rhizomatica/hermes-net/main` was rechecked on 2026-09-11 and still lacks that fix. Focused upstream resolution is tracked in Station issue #35, and the local patch/lifecycle gates must remain until an upstream replacement is accepted and the reciprocal acceptance is rerun.

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

### Station/client reconciliation (2026-09-21)

Confirmed merged with merge commits:

- [Station #47](https://github.com/OceanMail/oceanmail-station-archive/pull/47): readiness hardening, merge `65d75cb96b0b1247f598c49a60a11b8cba68e5b8`; current-base Phase 4I run `35559385475` passed on source `b001a11d085baa3b0bc3abe419f90f99034bf136`.
- [Project #35](https://github.com/OceanMail/oceanmail-project-archive/pull/35): ADR-007 HF capacity tiers, merge `4b77912bff1d3a36f136ee2c5ddd9f6cd4854c0b`.
- [Station #48](https://github.com/OceanMail/oceanmail-station-archive/pull/48): lab auth/context, merge `fac1ef575def8566dd6474f0a03f018a7cec4557`.
- [Desktop #22](https://github.com/OceanMail/oceanmail-desktop-archive/pull/22): lab context consumer, merge `339c73f3977e5cff849b00f4f221a5c64b336cfa`.
- [Desktop #24](https://github.com/OceanMail/oceanmail-desktop-archive/pull/24): bounded CI, merge `125b2b34da1c9d24f55634fb4655f67b27aa2e96`.
- [Project #36](https://github.com/OceanMail/oceanmail-project-archive/pull/36): implementation gates, merge `db260396b18db224117c95131162163fcdd7cece`.

The component source-head runs passed before merge. Desktop #24's regenerated
synthetic merge had no separate CI run; do not describe it as independently tested.
These merges accept laboratory implementation only, not production identity,
LAN access, private persistence, real Available, accounting, or physical radio.

Still open:

- [Desktop #23](https://github.com/OceanMail/oceanmail-desktop-archive/pull/23), head `486f06ab1da03bd11d5c42fbebe9c8ca2a97315f`: current-base run `35559386545` passed and the review finding is resolved. Actual Thunderbird Hold/Resume and attachment-only ordering acceptance remains outstanding. The owner authorized merging ready work on 2026-09-21; this remaining live acceptance gate is not CI failure or missing merge permission.
- Historical Server prototype #5 remains a carry-forward candidate with recorded failing PostgreSQL MFA evidence, not active Server implementation.

Station issues #23/#24 retain the production decisions recorded in
[`station-client-implementation-gates.md`](docs/specifications/station-client-implementation-gates.md).
No fixture or lab credential has been promoted to production private state.

Merged on 2026-09-11:

- Station PR #25: Debian trixie / Dovecot 2.4 compatibility and authenticated writable-IMAP `\Seen` transition proof.
- Station PR #26: logical Available manifest/account-authorization/retrieval-plan foundation and policy reconciliation.
- Station PR #27: project-spine integration and refreshed Station current-status documentation.
- Station PR #45: final chat-preservation consolidation for Grid accounting/metering, publication-readiness findings, and the retained single-radio operational baseline.

Open/follow-on work includes:

- issue #23: authenticated, permission-scoped Station API and stable account/user/device boundary;
- issue #24: account-scoped Available manifest, retrieval intent, and working-ledger API, blocked on #23;
- issue #22: implement ADR-008 Bands 0–3, capped control/route establishment, local/relay fairness and channel coordination within ADR-007 capacity-tier eligibility;
- issue #35: upstream HERMES reciprocal-session stale-TCP-tail report/fix while retaining the accepted local patch until an upstream replacement is proven;
- production storage encryption and per-user key separation remain unresolved release gates;
- Grid/control, relay/gateway execution, accounting/scheduling, API expansion, and physical-radio testing remain future bounded phases.

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

Desktop PR #7 is the current live-verified alpha baseline. Desktop PR #13 merged the Available/account/privacy contract reconciliation, PR #15 merged project-spine integration, and PR #21 merged the final chat-preservation design reconciliation for OChat evidence, consensual location/contact-card UX, Grid map/topology visualization, and Dashboard/gateway-policy presentation.

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

Server PR #3 and Infrastructure PR #3 merged the documentation/project-spine integrations on 2026-09-11. Their `main` branches already carry the centralized public SMTP/MX boundary; older reconciliation PRs that attempted to add the same boundary are superseded.

The architectural public-mail boundary is settled: OceanMail-operated Server/infrastructure is the only public Internet SMTP/MX authority. Remaining deployment work includes provider/hosting choice, host count/geography, IP/reputation operations, HA/recovery, and the authenticated Station/Server gateway contract. A central outage may delay Internet-boundary traffic, but native OMail must continue independently.

A still-open MFA carry-forward PR exists in `oceanmail-server-0.1-prototype`; it is not current Server main and must be deliberately ported/revalidated rather than treated as accepted active implementation.

## News / bounded low-bandwidth content

A preliminary News direction is preserved but is not implementation-ready. Initial Internet-side acquisition is bounded/curated, with RSS/Atom preferred where selected sources provide it and Server-side text-first normalization/provenance/source policy. Any future Grid caching must respect current STORE/TRANSPORT versus GRID/CONTROL boundaries and may not be used to justify speculative global mesh behavior. Source rights, object/manifest design, cache policy, scheduling/accounting, and measured compression/throughput remain unresolved before implementation.

## Publication/readiness state

The five active repositories remain private. The owner has prioritized preparing public fork/PR contribution, in this order: Project, Station, Desktop. Server and Infrastructure remain private. Outsiders normally receive no write access. Public PR validation uses standard GitHub-hosted runners; trusted self-hosted runner access must be excluded before conversion.

Master tracker: [#42](https://github.com/OceanMail/oceanmail-project-archive/issues/42); Project readiness: [#48](https://github.com/OceanMail/oceanmail-project-archive/issues/48). [Public collaboration policy](docs/specifications/public-collaboration.md) records settled direction. [Publication decisions](docs/specifications/publication-decisions.md) records approved code/docs license choices and zero required approvals; contribution/rights and application of settings remain pending. Current-tree/full-history secrets, privacy, provenance, GitHub surfaces, public CI and security/settings evidence remain gates. Current-tree privacy cleanup does not sanitize history. Desktop binary redistribution and production/RF readiness are separate boundaries.

## Historical/frozen repositories

- `oceanmail-0.1-prototype` — frozen historical prototype and design evidence.
- `oceanmail-server-0.1-prototype` — frozen historical hosted-service prototype.
- `oceanmail-infrastructure-0.1-prototype` — frozen historical deployment/operations prototype.
- `bempic` — frozen protocol research.
- `bempic-reference` — frozen reference implementation/research evidence.

The 0.1→0.2 transition record now preserves end-of-generation evidence, explicit non-evidence, carry-forward rules, BEMPIC/DCCL provenance, and historical licensing disposition without making any of it current 0.2 architecture. The initial BEMPIC M0 thread has a separate historical disposition recording its exact evidence boundary and reusable test lessons.

## Documentation-spine state

The organization-level spine migration and final accessible chat-history preservation audit are complete as of 2026-09-11:

- `oceanmail-project` owns organization-wide definition/architecture/decisions/state/workstreams/governance;
- active component READMEs/AGENTS/docs point to the central spine while implementation detail stays component-local;
- Desktop and Station final preservation PRs are merged;
- current state no longer lists already-merged Desktop PR #13 or Station PR #25 as open;
- historical/frozen repositories remain visibly non-current;
- residual accounting, publication, News, Grid terminology/UI, single-radio, and 0.1/BEMPIC historical knowledge has been routed to scoped durable documents rather than a generic chat dump.

Future chat reconciliation must continue to follow `docs/specifications/chat-reconciliation.md`; old conversation chronology never outranks newer accepted Git truth merely because a reconciliation happens later.

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

[Station PR #50](https://github.com/OceanMail/oceanmail-station-archive/pull/50) merged on 2026-09-22 as `ec9e5f232aac722bae25a979098100cc3c0dbaf9`, adding the first in-memory GRID/CONTROL lease policy slice for issue #22. Lease duration and normal control allowance are independent inputs, without selected ten/four-minute defaults or a fixed 40% ratio. All 22 local Rust tests passed on implementation head `edf036b9127f1e4c7258e721b8d98573d018386c`. Final source head `19610ba46c916eb01de83bb10053d30683972cf6` passed Phase 4J run `35744903091` and Phase 4I run `35744903108`; the numeric-default documentation finding is resolved. These are unit and existing integration-regression results, not live scheduler or RF validation. The controller is not connected to daemon transport dispatch. Persistent fairness/accounting, route-attempt backoff admission, traffic classification and channel coordination remain outstanding. GitHub issue #22 closed on 2026-09-22 despite PR #50 explicitly stating that its first slice does not close #22; a follow-up tracker is needed. Component contract: [LEASE_CONTROLLER.md](https://github.com/OceanMail/oceanmail-station/blob/main/docs/LEASE_CONTROLLER.md).

## Personal traffic and encryption decision (2026-09-22)

Band 1 is public discovery/route/access coordination plus authorized urgent public updates. Band 2 includes ordinary manifests, requests, receipts, custody/repair/stop-flow/tombstones, account reconciliation, and payload, with expedited mail control within its fairness shares. Bands 0/1/3 are public over HF. Client–own Station, direct Client–Server Internet, and gateway–Server connections are always authenticated and encrypted. Personal HF encryption, if adopted, terminates at Station and Server through untrusted relays/gateways; the deployed path has no plaintext capability or fallback. A single deployment choice remains pending feasibility, not a user or per-message option. External SMTP is a separate boundary without a universal encryption guarantee.

See [ADR-009](docs/decisions/ADR-009-personal-traffic-and-encryption.md). This records accepted design, not deployed encryption or traffic-classification evidence. Existing runtime/RF and production-security gates remain in force.

## CI retrofit coordination

[G0 / issue #43](https://github.com/OceanMail/oceanmail-project-archive/issues/43) registers the [rollout and measurement tracker](docs/specifications/ci-quality-retrofit.md). Station [S1 / issue #53](https://github.com/OceanMail/oceanmail-station-archive/issues/53) is first: report-only tooling and exact-head evidence. No baseline, required quality gate or branch enforcement is established by this governance work. Work beyond S1 awaits separate owner direction.


## Public-conversion audit evidence (2026-09-25)

[The audit record](docs/publication/2026-09-25-audit.md) records exact heads, hosted runs, history scan inventories, reviewed Station false positives and remaining owner/admin gates. All repositories remain private. No clean scanner result is treated as privacy, licensing or publication approval.

## Privacy cleanup (2026-09-26 UTC)

The owner requires removal of personal data and private runner details, with document review across all ten organization repositories. Current-file cleanup is distinct from historical Git identities/refs, discussions, logs/artifacts, archived material and cached copies. Those gates remain open; all five active repositories stay private. See DECISIONS.md and master #42.

