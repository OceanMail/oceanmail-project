# ADR-006 — Centralized Public Internet Mail Boundary

- Status: ACCEPTED
- Decision date: 2026-09-04
- Reconciled into project spine: 2026-09-11

## Context

OceanMail Stations can locally accept and emit standards-based email around the constrained-link transport and can act as OceanMail gateways when Internet connectivity is available. That capability does not require every gateway Station to become an independent public Internet mail server.

Distributing public SMTP delivery across vessel, volunteer, and managed gateway Stations would distribute reputation, credentials, bounce handling, abuse controls, retry policy, and deliverability risk across heterogeneous networks such as residential broadband, cellular, marina Wi-Fi, and satellite links.

At the same time, native OMail is intentionally a decentralized store-and-forward system and must remain useful when no Internet or OceanMail central service is available.

## Decision

OceanMail-operated Server/infrastructure is the only public Internet SMTP/MX boundary for OceanMail.

- Internet-connected Stations and gateway Stations do **not** deliver directly to arbitrary public Internet SMTP systems.
- Stations are not independent public Internet MTAs merely because they have Postfix, Internet connectivity, or gateway capability.
- A gateway Station moves eligible native OMail traffic toward/from OceanMail Server using the accepted OceanMail Station/Server service boundary.
- OceanMail Server/infrastructure performs conventional Internet-mail ingress/egress and owns the public-mail responsibilities: SMTP/MX, DKIM signing, SPF/DMARC alignment, Internet reputation, destination delivery/retry, bounce processing, abuse/rate controls, recipient/sender policy, and related operational monitoring.
- Exact provider, host count, geographic placement, IP allocation, and scale-out topology remain deployment decisions and may evolve without changing this architectural boundary.

## Native OMail remains decentralized

This decision does **not** centralize native OMail delivery.

A valid native path remains conceptually:

```text
Boat A Station
    -> constrained/native OMail transport
    -> relay/store-carry-forward Stations as available
    -> Boat B Station
    -> local standards-based mail client
```

No Internet access or central OceanMail Server is required for that path.

Central infrastructure is required only when traffic crosses between native OMail and conventional public Internet mail/services, or when a separately defined centrally managed service requires it.

## Failure behavior

If OceanMail Server/infrastructure is temporarily unreachable:

- gateway/Station work destined for the public Internet is retained in the appropriate durable store and retried rather than discarded;
- Internet-originated delivery may be delayed until an eligible OceanMail path becomes available;
- native boat-to-boat/store-carry-forward OMail continues independently wherever a viable native path exists.

A central outage therefore delays the Internet boundary; it must not disable native OMail as a whole.

## Consequences

### Benefits

- one controlled public-mail reputation surface;
- centralized DKIM/SPF/DMARC and deliverability operations;
- simpler Station trust and configuration;
- no requirement to distribute public-SMTP relay credentials to gateway Stations;
- reduced abuse surface if a volunteer/private Station is compromised;
- centralized bounce/retry policy and observability;
- heterogeneous gateway access networks do not directly determine OceanMail's public SMTP reputation.

### Costs

- public Internet mail depends on OceanMail-operated infrastructure being eventually reachable;
- Server/infrastructure owns additional queueing, policy, and operational responsibility;
- high availability and recovery of the Internet-mail boundary matter more as usage grows.

The expected OceanMail message profile makes the compute/storage cost of central mail handling modest relative to the operational simplification; scale-out remains evidence-driven.

## Rejected alternative

Rejected: make Internet-connected gateway Stations public MTAs, either by direct destination SMTP delivery or by giving every gateway privileged access to a central smarthost.

A secure per-Station authenticated smarthost design could be built, including per-Station certificates and centralized reputation, but it adds credentials, authorization, abuse attribution, public-mail retry/bounce concerns, and configuration to every gateway without preserving any native OMail capability that would otherwise be lost.

This rejected design must not be reintroduced merely because Station already uses SMTP/Postfix locally. Local SMTP boundaries and public Internet MTA responsibility are different concerns.

## Related documents

- `PROJECT.md`
- `DECISIONS.md`
- `docs/decisions/ADR-003-client-station-server-boundaries.md`
- `docs/decisions/ADR-004-station-store-transport-grid-control.md`
- `docs/decisions/ADR-005-delivery-evidence-and-repair.md`
- `docs/interfaces/component-boundaries.md`
- `workstreams/server.md`
- `workstreams/infrastructure.md`
- `workstreams/station.md`
