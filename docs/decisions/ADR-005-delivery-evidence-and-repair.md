# ADR-005 — Evidence-Based Delivery Confirmation and Bounded Repair

Status: **ACCEPTED**

Date: 2026-09-11

## Context

OceanMail operates across intermittent links where a sender may successfully hand data to another Station, lose the return path before acknowledgement, or wait a long time while the destination/relay is simply offline. A local transport/session success therefore cannot safely mean that the intended destination received the message.

At the same time, blindly retransmitting payload whenever a receipt is late would waste constrained airtime and, once relay/multi-hop behavior exists, could create uncontrolled copies throughout the network.

Station Phase 4I already proves a compact returned receipt can traverse the no-radio HERMES/Mercury path and be correlated back to the original message/job. That proof is laboratory transport evidence at trust `lab_peer_transport_unverified`, not production cryptographic trust.

## Decision

OceanMail delivery and repair semantics are evidence-based:

1. **An intermediate handoff is not final delivery.** Queue departure, transport progress/session success, gateway/relay acceptance, and final authoritative destination receipt remain distinct evidence states.
2. **Sender-visible delivery confirmation requires returned authoritative destination evidence** for the applicable delivery objective. Human reading is separate.
3. **One user message keeps one stable logical OMail identity across retries.** Lower-layer jobs, transport attempts, routes, or dissemination epochs may change without creating a second logical email.
4. **Missing final evidence means unknown, not failed.** Ordinary repair uses patience/backoff because a vessel, relay, or return path may legitimately be unavailable for hours or longer.
5. **Probe before expensive re-injection when practical.** If prior work appears stale, query available authoritative/authorized state before resending the payload. Positive evidence, explicit negative evidence, and no response are separate outcomes.
6. **Automatic repair is bounded.** A justified reattempt uses the same logical message under a new attempt/epoch. Repeated uncertainty eventually requires longer backoff, a materially new opportunity, or user attention rather than infinite hidden retransmission.
7. **Compact delivery receipts/tombstones may outlive large payload caches.** This suppresses stale re-injection after ordinary relay/cache state has expired.
8. **Future relay propagation must be bounded and relevant.** If/when multi-hop relay execution is approved, relay responsibility is not final delivery; passive listeners do not automatically become payload caches; ordinary traffic must not reproduce epidemically around the planet merely because distant Stations can hear it.

Detailed semantics are in [`../specifications/delivery-evidence-and-repair.md`](../specifications/delivery-evidence-and-repair.md).

## Consequences

- Desktop/client delivery UI must not infer destination receipt from local queue or transport state.
- Station must correlate OceanMail logical identity with lower-layer jobs/attempts/evidence while leaving authoritative payload queues in their existing store/transport owners.
- Server may answer repair/delivery questions only for state it authoritatively owns or can evidence.
- Receipts/control evidence can be treated as high-value system microtraffic because they can suppress substantially larger retransmission.
- Current multi-hop implementation remains deferred/evidence-gated. This ADR defines semantics that any later implementation must satisfy; it does not authorize a global routing layer.
- Production receipt authentication/signing, retry timers, retry-count limits, relay responsibility counts/leases, exact tombstone lifetime, and accounting treatment remain separate implementation/policy decisions.

## Superseded / rejected interpretations

- **Delete-on-handoff:** rejected. A next-hop/relay acceptance is not enough evidence to destroy the source's only recoverable copy.
- **No receipt means immediate failure:** rejected.
- **Every retry becomes a new email:** rejected.
- **Blind global caching/epidemic payload replication:** rejected as a future relay policy.
- **Old BEMPIC/M4P ownership assumptions:** superseded. Current HERMES/Mercury STORE/TRANSPORT and OceanMail GRID/CONTROL boundaries remain authoritative.