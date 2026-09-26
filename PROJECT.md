# OceanMail Project Definition

## What OceanMail is

OceanMail is a maritime communications product and service for intermittent, low-bandwidth, high-latency, expensive, metered, and opportunistic connectivity while remaining useful over ordinary Internet connections.

OceanMail 0.2 is an upstream-first system built around four primary boundaries:

- **OceanMail Desktop / future clients** — user-facing mail and communications experience.
- **OceanMail Station** — autonomous onboard/edge communications, persistence, policy, evidence, and Grid/control service.
- **OceanMail Server** — hosted Internet-side accounts, mailbox/service functions, the authoritative public Internet-mail boundary, and server-authoritative service policy/accounting.
- **OceanMail Infrastructure** — deployment, operations, DNS, CI/CD, monitoring, backup/recovery, and supply-chain controls.

The communications foundation uses HERMES-derived store/transport behavior and Mercury first, with additional supported transports behind the Station boundary where justified.

## Stable principles

1. **Git is authoritative project memory.** Chat history, agent memory, and verbal handoffs are not architecture authority.
2. **Client, Station, Server, and Infrastructure are separate architectural components** even when deployed together.
3. **Upstream first.** OceanMail does not recreate modem DSP, generic ARQ/FEC, UUCP behavior, or radio-control internals when maintained upstream components satisfy the requirement.
4. **Evidence must be truthful.** Queue disappearance, transmit progress, gateway acceptance, remote mailbox receipt, and human reading are different claims and must not be conflated.
5. **Privacy and authorization remain explicit boundaries.** Station administration or device trust does not automatically grant another user's mailbox/private metadata access.
6. **Standards where they fit; OceanMail APIs where they do not.** SMTP/IMAP may carry ordinary local mail behavior. OceanMail-specific state such as Available manifests, Grid state, account-scoped budgets, and Station controls belongs behind authenticated OceanMail APIs/contracts.
7. **Native OMail preserves decentralized capability.** Boat-to-boat/store-carry-forward native OMail must not depend on Internet access or central Server availability.
8. **Public Internet mail is centralized.** Only OceanMail-operated Server/infrastructure is the public SMTP/MX boundary; Internet-connected Stations/gateways do not become independent public MTAs or deliver directly to arbitrary Internet SMTP systems.
9. **Complex networking is evidence-gated.** Prove direct gateway/service operation first; dynamic gateway selection and multi-hop forwarding require measured need.
10. **Emergency is exceptional.** Emergency is the only current user-originated mail class that changes transport precedence; ordinary `Important` is metadata only.
11. **Present truth is separated from history.** Current documents describe what is true now; ADR/history documents preserve why and what was superseded.

## Major system relationships

```text
OceanMail Desktop / future clients
       | \
       |  \ direct Internet, where supported
       |   ------------------------------> OceanMail Server
       |
       | authenticated Station API + local SMTP/IMAP where applicable
       v
OceanMail Station
       |
       +--> HERMES UUCP/uucpd/uuxcomp baseline
       |       +--> Mercury
       |       +--> VARA / ARDOP / PACTOR / future supported links
       |
       +--> ordinary IP/Internet
       |
       `--> accepted relay / OceanMail gateway behavior
                    |
                    v
             OceanMail Server
             public SMTP/MX boundary
                    |
                    v
          conventional Internet mail/services
```

Native OMail paths may terminate at another Station without traversing OceanMail Server. Server participation is required when crossing to/from conventional public Internet mail/services, not for native boat-to-boat delivery.

## What OceanMail is not

OceanMail 0.2 is not:

- the old mandatory `OceanMail -> BEMPIC -> M4P -> DataLink` stack;
- a new clean-sheet HF modem/DSP project;
- a commitment to global speculative mesh/multi-hop forwarding before field evidence;
- a design in which every Internet-connected Station becomes an independent public SMTP server;
- a general-purpose arbitrary Internet-mail client during the current Desktop 0.x scope;
- a claim that laboratory no-radio evidence equals live RF or production-security proof;
- a design in which a handoff, issue, PR description, or AI conversation silently overrides accepted architecture.

## Authority

Organization-level architecture and decisions live in this repository. Detailed implementation truth lives in the owning component repository. See [`REPOSITORIES.md`](REPOSITORIES.md) and [`docs/interfaces/component-boundaries.md`](docs/interfaces/component-boundaries.md).