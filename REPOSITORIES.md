# OceanMail Repository Inventory


Updated: 2026-09-26

Status terms: **ACTIVE**, **BOOTSTRAP**. All five repositories below are public.

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

## Upstream dependencies, not OceanMail repositories

OceanMail currently consumes upstream communications projects rather than maintaining organization forks by default. Station documentation pins exact accepted versions/commits where required.

Key upstream families include:

- Rhizomatica HERMES networking/UUCP integration;
- Rhizomatica Mercury;
- related HERMES radio/broadcast work where later justified;
- other supported transport/modem projects such as VARA/ARDOP/PACTOR integrations where technically and legally appropriate.

## Repository-boundary rule

If a fact is organization-wide, place it in `oceanmail-project`. If it is an implementation detail of one component, place it in that repository and link to it from the spine only when orientation requires it.

This inventory lists the five public repositories that contributors need.


## Public contribution

All five repositories are public with installed licenses and protected `main`. See [PUBLICATION.md](PUBLICATION.md) and [CONTRIBUTING.md](CONTRIBUTING.md).
