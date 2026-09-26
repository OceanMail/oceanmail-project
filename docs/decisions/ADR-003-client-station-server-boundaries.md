# ADR-003 — Client, Station, Server, and Infrastructure Boundaries

- Status: ACCEPTED
- Centralized: 2026-09-11
- Preserves current 0.2 component model previously documented in Desktop scope/architecture and active component READMEs

## Decision

OceanMail uses four separate architectural responsibilities:

### Client/Desktop

Owns user-facing product interaction and client behavior. It may use direct Internet access to the hosted service and/or a local Station. A client is not automatically a Station, relay, or gateway merely because it has storage/network access.

### Station

Owns persistent onboard/edge communications, transport observation/evidence translation, OceanMail policy/state needed for autonomous work, authenticated Station-specific APIs, and Grid/control evolution. It may run headless and serve multiple clients.

### Server

Owns hosted accounts/authentication/mailbox/service behavior, service-side APIs/jobs, the authorized conventional Internet-mail bridge, and server-authoritative accounting/abuse/billing/service policy.

### Infrastructure

Owns deployment and operations: environments, DNS/TLS/networking, CI/CD, backups, monitoring, secret-management boundaries, and supply-chain controls.

## Mail boundary

Native OMail remains decentralized and may move boat-to-boat/store-carry-forward without central Server availability. When traffic crosses between native OMail and conventional public Internet mail, OceanMail-operated Server/infrastructure is the sole public SMTP/MX boundary. Gateway Stations move eligible OMail traffic toward/from that boundary; they do not become independent public Internet MTAs merely because they have Internet connectivity or local SMTP/Postfix capability.

Exact production provider, host count, geographic placement, IP allocation, and scale-out topology remain implementation/deployment decisions. See ADR-006.

## Consequences

- missing Station capabilities must not be fabricated in Desktop;
- Infrastructure must not redefine product semantics to simplify deployment;
- Server remains transport-neutral with respect to lower-layer RF/modem behavior;
- standard SMTP/IMAP and OceanMail-specific APIs are complementary rather than mutually exclusive;
- local Station SMTP service is not equivalent to public Internet MTA authority;
- central Internet-mail outages may delay Internet-boundary work but must not disable viable native OMail paths.