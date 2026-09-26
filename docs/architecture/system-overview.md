# OceanMail 0.2 System Overview

Status: CURRENT

OceanMail separates product/client behavior, persistent onboard communications, hosted service behavior, and operations into distinct components.

```text
Client/Desktop
  |-- direct Internet --------------------> Server
  |
  `-- local authenticated boundary ------> Station
                                            |
                                            |-- HERMES/Taylor UUCP -> Mercury/other link
                                            |-- ordinary IP
                                            `-- accepted relay/gateway behavior
                                                       |
                                                       v
                                                     Server
                                                       |
                                                       v
                                             external Internet mail/services
```

## Desktop/client

Uses Thunderbird as the Desktop implementation foundation. It owns user experience and client-side OceanMail semantics, not modem/radio internals. Standard SMTP/IMAP are reused where they represent normal local mail behavior; OceanMail-specific state uses Station/Server APIs/contracts.

## Station

Persistent headless edge service. It may continue communications work while clients are disconnected. It owns OceanMail policy/evidence metadata and Grid/control evolution while avoiding duplicate payload queues already authoritatively owned by Postfix, Taylor UUCP, Dovecot/mailbox storage, HERMES/Mercury, or later store/transport components.

Current Station architecture distinguishes:

- **STORE / TRANSPORT** — durable holding/movement of accepted traffic and transport/receipt evidence.
- **GRID / CONTROL** — peer/Grid observations, relay/gateway policy, topology, telemetry/reputation inputs, OChat Grid behavior, maps/network state, and future selection/routing intelligence.

## Server

Hosted service/application boundary for accounts, authentication, hosted mailbox/service state, external Internet-mail handoff, service APIs/jobs, and server-authoritative policy/accounting/abuse/billing behavior.

## Infrastructure

Operational/deployment boundary. It may impose operational constraints but must surface conflicts rather than redefining application/product semantics.

## Communications foundation

HERMES/Mercury is upstream-first. The current proven no-radio baseline uses standard mail + Postfix + HERMES `uuxcomp` + Taylor UUCP + HERMES UUCP endpoints + Mercury + remote Postfix/Dovecot/mailbox behavior. Real RF remains a later proof phase.

## Deferred networking complexity

Direct gateway/service behavior comes first. Dynamic gateway selection follows when justified. Multi-hop Station-to-Station forwarding is not presumed; it requires field evidence and a deliberate decision.