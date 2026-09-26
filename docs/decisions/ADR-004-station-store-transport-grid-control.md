# ADR-004 — Station STORE/TRANSPORT and GRID/CONTROL Separation

- Status: ACCEPTED
- Original decision: 2026-09-04
- Centralized: 2026-09-11
- Current semantics reconciled through: 2026-09-10

## Context

OceanMail Station combines two materially different responsibilities:

1. durable holding/movement of accepted traffic and truthful transport/receipt evidence; and
2. understanding the OceanMail network and deciding how the Station should behave within it.

Blurring those responsibilities would make it easy to push OceanMail-specific relay, gateway, OChat, reputation, or routing policy into HERMES, Mercury, Taylor UUCP, Postfix, Dovecot, or another store/transport component merely because that component happens to hold or move bytes.

The original September 4 discussion called the first side the **Mail / Transport Plane**. Current Station terminology is **STORE / TRANSPORT Plane** because the boundary also covers coordination of authoritative durable stores/queues and evidence, not only transmission of email.

## Decision

OceanMail Station has three logical internal domains:

```text
                       OceanMail Station
                              |
                    +---------+---------+
                    |   Station Core    |
                    | identity/config   |
                    | API/events/state  |
                    +---------+---------+
                              |
              +---------------+---------------+
              |                               |
              v                               v
    STORE / TRANSPORT Plane          GRID / CONTROL Plane
```

### STORE / TRANSPORT Plane

Owns or coordinates execution of accepted communications work and the evidence produced by that execution. This includes integration with authoritative stores/transport components such as Postfix, Dovecot/mailbox storage, HERMES, Taylor UUCP, Mercury, ordinary IP, and future accepted HF/VHF/IP adapters.

OceanMail-owned Station state may persist mappings, policy decisions, budgets, evidence, and metadata, but it must not create a parallel payload queue when an existing component already owns the authoritative durable payload/store state.

### GRID / CONTROL Plane

Owns OceanMail-specific network intelligence and policy: peer/station observations, topology, relay policy, gateway policy, OChat Grid behavior, reputation/telemetry inputs, map/network state, and future path/route-selection intelligence.

### Station Core

Provides shared identity, configuration, authorization, API/event boundaries, and cross-plane state. The split is logical; it does not require separate executables or machines.

## Policy/execution contract

The architectural rule is:

> **GRID / CONTROL decides what the Station should do; STORE / TRANSPORT carries out accepted work and reports what actually happened.**

Examples of GRID / CONTROL decisions include selecting a peer/gateway, accepting relay custody, applying Emergency precedence and ordinary fairness, and deciding whether Station resource policy permits work.

STORE / TRANSPORT reports measurable evidence back: peer/link used, bytes moved where measurable, timestamps, success/failure, queue/store state, and transport/receipt evidence. It must not invent Grid policy or stronger delivery claims than its evidence supports.

## Relay, gateway, and OChat placement

Relay and gateway modes are GRID / CONTROL policy, while accepted relay/gateway transfers are executed through STORE / TRANSPORT.

Current relay/gateway semantics are recorded in `DECISIONS.md` and the Station component documentation. In particular:

- a running Station has no relay `Off` mode;
- Eager relays advertise availability, subject to Station resource controls;
- Reluctant relays do not advertise and intervene only as fallback under accepted Grid policy;
- gateway policy is independent of relay willingness and uses Full, Minimal, and Off for ordinary third-party gateway service;
- Emergency remains eligible under OceanMail policy in every relay/gateway mode when technically capable and legally/operationally permitted.

OChat is a GRID / CONTROL service using shared STORE / TRANSPORT resources. It is not durable OMail store-and-forward traffic. OMail may preempt OChat, eager/reluctant relay modes do not govern ordinary OChat forwarding, and OChat airtime/resource policy remains a separate Grid concern.

## Superseded details

Two details from the original September 4 design discussion are intentionally not current truth:

1. **`Mail / Transport Plane` terminology** was broadened to **`STORE / TRANSPORT Plane`** so the boundary explicitly includes authoritative durable stores/queues and evidence correlation.
2. The original **Minimal/Priority Gateway** concept depended on an ordinary sender-selectable Priority class. That class was removed by the later Emergency/Ordinary decision. Minimal Gateway now means fallback for stranded/stalled **Ordinary** third-party traffic when Grid policy finds no suitable Full Gateway/route or excessive delay has accumulated. `Important` metadata and credits do not create transport precedence or affect gateway selection.

The September 4 rejection of a relay `Off` mode remains current.

## Consequences

- HERMES, Mercury, Taylor UUCP, Postfix, Dovecot, and future store/transport adapters remain focused on their transport/store responsibilities rather than absorbing OceanMail Grid policy.
- Grid policy can evolve without rewriting lower-layer transport implementations.
- New transports can be added behind STORE / TRANSPORT without changing the meaning of Eager/Reluctant relay, gateway modes, or OChat policy.
- OChat must not be modeled as durable mail simply because it uses the same radio/IP resources.
- The Station component repository remains authoritative for implementation details, exact current behavior, evidence, and future thresholds/timers. This ADR owns the organization-level architectural separation and placement of responsibilities.
