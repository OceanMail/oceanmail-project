# OceanMail Repository Inventory

> Publication scope update — 2026-09-26: the owner approved fresh public repositories for **all five active components: Project, Station, Desktop, Server and Infrastructure**. Preserve the original repositories privately with `-archive` suffixes. The five older BEMPIC/0.1 repositories remain private and frozen. Earlier three-repository scope statements below are superseded historical records.


> Current publication decision (2026-09-26): create fresh sanitized Project, Station and Desktop repositories with installed licenses. Preserve the original repositories privately under names ending in `-archive`. See [PUBLICATION.md](PUBLICATION.md). Earlier in-place conversion instructions and pending-license statements below are historical.


Updated: 2026-09-25

Status terms: **ACTIVE**, **BOOTSTRAP**, **FROZEN RESEARCH**, **HISTORICAL**.

## Organization and naming conventions

The dedicated `OceanMail` GitHub organization is the canonical home for OceanMail project repositories. OceanMail is not placed under another project organization merely to share runners or other organization-scoped infrastructure.

Active component repositories use explicit component names. In particular, the Desktop implementation is `OceanMail/oceanmail-desktop`; there is intentionally no active generic `OceanMail/oceanmail` repository whose purpose could be confused with the overall project or organization.

## Active project and implementation repositories

| Repository | Status | Purpose / authority | Major relationships |
|---|---|---|---|
| `OceanMail/oceanmail-project` | ACTIVE | Organization-level project memory, current architecture, terminology, repository inventory, cross-repository decisions, workstreams, agent governance. | References all component repositories; does not own component source code. |
| `OceanMail/oceanmail-desktop` | ACTIVE | Thunderbird-based OceanMail Desktop implementation and client-specific product behavior/docs. | Uses Station API + local SMTP/IMAP where appropriate; may use Server directly over Internet for supported functions. |
| `OceanMail/oceanmail-station` | ACTIVE | Autonomous onboard/edge Station, evidence/policy/state, HERMES/Mercury integration, Grid/control evolution, local service/API. | Integrates upstream HERMES/Mercury; serves Desktop; later synchronizes with Server/gateways. |
| `OceanMail/oceanmail-server` | BOOTSTRAP | Hosted accounts/auth/mailbox/service APIs, external Internet-mail handoff, server-side accounting/abuse/billing boundaries. | Consumed by clients/Stations; external conventional Internet mail lives beyond this boundary. |
| `OceanMail/oceanmail-infrastructure` | BOOTSTRAP | Deployment, CI/CD, DNS/TLS/networking, monitoring, backup/recovery, secrets/supply-chain and operations. | Deploys Server and future hosted/gateway infrastructure without redefining product semantics. |

### Primary authoritative documentation locations

- Project: root project files, `docs/`, `workstreams/`, `handoffs/`.
- Desktop: root `AGENTS.md`, `README.md`, current `docs/`, and `desktop/docs/` for implementation-specific evidence.
- Station: root `AGENTS.md`, `README.md`, `docs/CURRENT_STATUS.md`, `docs/STATION_ARCHITECTURE.md`, security/upstream/contract documents.
- Server: `README.md`, `docs/README.md`, and future implementation docs as created.
- Infrastructure: `README.md`, `docs/README.md`, and future deployment/operations docs as created.

## Frozen/historical repositories

| Repository | Status | Purpose / warning |
|---|---|---|
| `OceanMail/bempic` | FROZEN RESEARCH | BEMPIC protocol research. Frozen 2026-09-02; not an active OceanMail 0.2 dependency. Specification remains normative only for the frozen BEMPIC research state. Its `GREAT_PARALLEL_WORK.md`, `docs/PRIOR-ART-AND-BOUNDARIES.md`, B2F/LZHUF comparison material, M4P notes, and protocol metrics preserve useful prior-art research without making it current architecture. |
| `OceanMail/bempic-reference` | FROZEN RESEARCH | Experimental BEMPIC reference implementation/conformance evidence; no stable production wire format and not active 0.2 implementation. |
| `OceanMail/oceanmail-0.1-prototype` | HISTORICAL | Former clean-sheet OceanMail 0.1 product/UI/architecture prototype. Useful design history; current 0.2 architecture overrides conflicts. Its `GREAT_PARALLEL_WORK.md` is the retained research register for historical Winlink/B2F, SailMail/AirMail, M4P, Reticulum, PACTOR/VARA/ARDOP, DTN, ALE and related investigations; those entries are prior art, not active 0.2 commitments unless separately accepted in the spine. |
| `OceanMail/oceanmail-server-0.1-prototype` | HISTORICAL | Former hosted-service prototype. Contains useful auth/queue/security work, but not current Server authority. Open carry-forward work must be deliberately ported/revalidated. |
| `OceanMail/oceanmail-infrastructure-0.1-prototype` | HISTORICAL | Former deployment/operations prototype. Use historical runbooks/security lessons selectively; do not deploy from it as current authority. |

### Historical repository handling

As of the 2026-09-11 reconciliation, the five frozen/historical repositories above have no active `.github/workflows` directory, so they cannot accidentally consume the shared OceanMail self-hosted runner through their old CI definitions.

Live GitHub metadata verified 2026-09-22 reports `archived=true` for all five frozen/historical repositories. This supersedes the September 11 `archived=false` observation. The five active repositories remain unarchived. See the [recorded inventory](docs/quality/inventory-2026-09-22.json). Archives remain excluded from execution and retrofit changes; deliberate ports require validation in the active destination.

## Upstream dependencies, not OceanMail repositories

OceanMail currently consumes upstream communications projects rather than maintaining organization forks by default. Station documentation pins exact accepted versions/commits where required.

Key upstream families include:

- Rhizomatica HERMES networking/UUCP integration;
- Rhizomatica Mercury;
- related HERMES radio/broadcast work where later justified;
- other supported transport/modem projects such as VARA/ARDOP/PACTOR integrations where technically and legally appropriate.

## Repository-boundary rule

If a fact is organization-wide, place it in `oceanmail-project`. If it is an implementation detail of one component, place it in that repository and link to it from the spine only when orientation requires it.

Historical repositories must remain visibly historical/frozen. A new contributor must never have to infer current authority from repository age, commit activity, or GitHub's archive toggle.


## Public-contribution preparation

All five active repositories remain private at the 2026-09-25 audit. Owner update 2026-09-25: prepare public conversion only for Project, Station and Desktop, in that order. Server and Infrastructure remain private. Privacy/document review covers all ten repositories. Each must pass [publication gates](docs/specifications/publication-readiness.md). No visibility conversion has passed yet. Historical visibility is deferred. See [master #42](https://github.com/OceanMail/oceanmail-project-archive/issues/42).
