# ADR-008 — Four-band scheduling and channel use

Status: ACCEPTED DESIGN; scheduler/channel implementation and runtime validation remain outstanding.
Date: 2026-09-21
Amended: 2026-09-22 by [ADR-009](ADR-009-personal-traffic-and-encryption.md): ordinary mail metadata/control moves to Band 2; Bands 0/1/3 are public over HF.
Authority: owner's final four-band cap-and-remainder decision and approval of channel behavior.

## Context and supersession

The owner replaced the earlier six-band proposal, the subsequent reserved 2/6/2-minute model, and the rule that no ordinary band could occupy an entire lease. Those drafts remain in PR/commit history; they are not current requirements.

This decision also supersedes Desktop Decision 0009's older five-band hierarchy. Emergency/Ordinary transport classes, Important-as-metadata, recipient selection, authorization, and fair scheduling remain in force. Band numbers are scheduler categories, not user-selectable priority classes.

## Current bands

| Band | Purpose | Airtime behavior |
| --- | --- | --- |
| 0 | Emergency payload and its own propagation/control | Preempts all other bands and overrides ordinary byte/time budgets. |
| 1 | Public Grid updates, discovery, route/access coordination, and urgent Server-designated public shared updates | May use the full lease for necessary route establishment. Once a route exists, the independently configured normal Band 1 cap applies. |
| 2 | Ordinary local-account and third-party relay mail service, including personal metadata/control and payload | Uses the remaining available lease time, with internal local/relay and account/peer fairness. |
| 3 | Shared background broadcast data | No reserved lease time. Uses idle opportunities or announced update broadcasts when there is a need. |

Owner clarification, 2026-09-21: the ten-minute lease and four-minute normal Band 1 cap were arithmetic examples, not selected defaults. Lease duration and normal control allowance are independent configurable values; no fixed 40% relationship is established. Operating defaults await measured transport overhead, throughput, and responsiveness. The settled relationship is a normal Band 1 cap, a necessary route-establishment exception, Band 2 using the remainder, and no Band 3 reservation.

Each band has its own internal order. Emergency stop-flow/tombstones stay in Band 0; ordinary mail control, manifests, bodies, and selected attachments are Band 2; public network coordination is Band 1; ordinary shared datasets/configuration/software/firmware are Band 3.

## Lease behavior

A lease is a finite agreed shared-radio opportunity, not guaranteed connectivity or a global network-wide entitlement. Negotiation/ACK/retry/switching overhead must fit within its duration where it occupies that opportunity. A Station releases the channel early when no eligible work remains; it does not transmit filler or hold unused time.

Band 1 may use the entire lease when required to establish a usable route for queued work. At lease expiry it yields; unfinished route work may continue in a subsequent lease. A usable next hop suffices for accepted store-and-forward operation; this is not a requirement to establish an end-to-end circuit or contact the Server before every native transfer.

Once the route is established, Band 1 returns to its normal cap. Ordinary manifest refresh, routine reconciliation, and distribution of an urgent update do not themselves qualify as route establishment. Repeated unsuccessful setup needs bounded attempts, progress evidence, and backoff so an unreachable destination cannot consume successive leases indefinitely. Exact progress/time thresholds remain implementation tuning.

Band 2 can use all time remaining after actual Band 1 work and necessary overhead; unused Band 1 time is not artificially withheld. For example, in a ten-minute lease, one minute of Band 1 leaves up to nine minutes for Band 2. If Band 1 has no work, eligible Band 2 work may use the whole usable lease. The former blanket prohibition on a full-lease ordinary band is explicitly withdrawn.

Band 3 has no guaranteed minimum, no 2-minute reservation, and no mandatory demand poll that reserves a share of every directed lease. It may use idle opportunities or separately announced broadcast windows. Bulk data is not forced onto a degraded link merely because time is idle; capacity-tier eligibility still applies.

## Band 0 emergency mode

Band 0 has its own propagation announcements, coordination, payload, acknowledgements, stop-flow, deduplication, and tombstone management. These records do not wait for Band 1. Within Emergency delivery, likelihood of loss of life precedes age among equally severe items; images remain layered.

All technically capable and authorized participating Stations follow the emergency coordination mechanism even when ordinary willingness/budget settings would defer service. Emergency retains existing authentication/authorization and legal/operational gates; neither the label nor a scheduler grant creates permission to transmit.

The intended behavior is coordinated collision avoidance with defined transmit/forward/listen roles, not every Station transmitting at once. The actual Emergency access/propagation protocol, duplicate suppression, stop-flow validation, and bounded detection/preemption latency must be designed and tested. Band numbering alone does not prove collision-free operation.

## Band 1 ordering and Server promotion

Within Band 1, route repair and necessary access coordination precede routine advertisements and Grid maintenance. Ordinary message-specific stop-flow, delivery evidence, tombstones, manifests, requests, and reconciliation belong in Band 2. Coalesce/rate-limit routine updates so they do not crowd out critical control.

The Server may designate normally background shared data as urgent, for example a security update or piracy notice, and assign its distribution to Band 1. Honor only authenticated, authorized Server designations with validated scope/freshness; an ordinary sender cannot gain this treatment by setting Important or relabeling a payload. Promotion does not make the item Band 0 and does not grant the route-establishment full-lease exception. The normal Band 1 cap applies to promoted distribution.

Source authentication, revocation/freshness, and detailed internal ordering of competing urgent updates remain implementation contracts; no wire format or production cryptography is chosen here.

## Band 2 mail control and internal order

Band 2 includes account manifests/Available metadata, retrieval requests, inventories, partial/resume state, custody evidence, destination receipts, repair/status probes, ordinary stop-flow/tombstones, mailbox and usage-accounting reconciliation, bodies, and selected attachments. Band 1 retains Station-level channel/time negotiation and airtime grants; message-specific selection is Band 2.

Process compact evidence that suppresses redundant work first, then enough manifests/requests/resume state to choose useful work, then bounded payload batches with resulting evidence and control reconsidered between batches. Do not drain every manifest before serving any payload. New stop-flow/delivery evidence receives expedited processing at the next safe transport boundary. Essential transport ACKs remain with their exchange. See [ADR-009](ADR-009-personal-traffic-and-encryption.md).

## Band 2 fairness and relay service

Local ship/captain/crew mail service and third-party relay mail service, including their metadata/control and payload, share Band 2. Maintain internal fairness between local and relay work, account fairness within local work, and per-requesting-Station fairness within relay work. An idle group's unused capacity can serve the other group. Exact local/relay weights or minimum shares remain tunable; the earlier 4/2-minute example is not a fixed allocation.

Use bounded turns and persistent age/service accounting across leases. For five continuously eligible relay peers, equal airtime shares of the available relay service are an initial policy, not an entitlement to one-fifth of every contact. Idle-peer shares may be reused. Slower links transfer fewer bytes for the same time; extra sessions/reconnects must not create additional shares.

Measure incoming acceptance and onward-forwarding cost. Bound new custody against sustainable forwarding airtime, route availability, storage, and backlog while preserving responsibility for already accepted work. Stable authorized Station identity and multi-hop attribution remain production prerequisites.

For local accounts retain ship/captain/crew service order with round-robin fairness, size-tier ordering, FIFO within tiers, and aging protection. Honor recipient-selected Available order within the account's share. Body text precedes attachments; selecting an attachment also requests its body unless already present. Large attachments require bounded supported pause/resume/batch boundaries rather than monopolizing a contact.

Stations automatically synchronize authorized manifests/applicable metadata. Ordinary content retrieval requires explicit recipient selection, and accepted work may continue after client disconnect. Possession of a relay copy grants no local mailbox access.

Downstream request generation, upstream admission/fair scheduling, and their shared request/grant exchange are separate responsibilities. Demand is not a grant; repeated requests update existing demand. A directed grant identifies participants, permitted work/direction, duration, and validity, subject to both Stations' eligibility and actual channel access. Both local and relay ordinary payload now classify as Band 2; their internal accounting/fairness scopes still differ.

## Channel behavior

Bands are scheduling policy, not mandatory one-band-per-frequency channels. The single-radio baseline uses:

| Activity | Channel behavior |
| --- | --- |
| Discovery and announcements | A rendezvous channel carries presence, contact requests, and time/channel announcements for upcoming exchanges. |
| Directed exchange | Participants negotiate a channel, perform necessary addressed Band 1 exchange, and then Band 2 mail control/metadata and payload there. No obligatory frequency change separates control from its associated payload. |
| Shared update broadcast | A Station holding updates announces time, channel, dataset/version, and expected duration. Interested idle Stations tune in. Ordinary data is Band 3; authenticated Server-promoted urgent data receives Band 1 precedence. |

An hourly update opportunity may be arranged when shared updates exist. This is not an unconditional hourly RF reservation or a return to Band 3 lease slices. One announcement can coordinate many listeners rather than requiring repeated addressed downloads. Broadcast source selection, announcement conflicts, and collision avoidance remain implementation work.

Where the modem/link supports decoding or monitor/broadcast reception, public Grid records and shared datasets may be overheard and reused after validating source, integrity, and freshness. Addressed private manifests retain account/holder authorization; overhearing does not authorize local API disclosure. Ordinary Band 2 traffic is not public merely because it is observable over radio.

Listening to a payload transfer does not confer relay custody, permission to send ACKs, or permission to join its transmission schedule. Participation/custody requires explicit coordination.

A single radio cannot monitor rendezvous/Emergency activity while tuned to another channel. Directed exchanges and broadcasts therefore need bounded listening/check-in opportunities and a tested Emergency discovery/preemption mechanism. Announced broadcasts yield to Emergency. Do not claim instantaneous cross-channel preemption or collision-free propagation from priority labels alone.

Essential link-layer ACKs and safe teardown remain part of the exchange they support; do not wait for a later Band 1 turn and deadlock the transport. HERMES/Mercury/UUCP retain ARQ, framing, modem adaptation, and authoritative payload-store ownership.

## Capacity and accounting boundaries

User/ship accounts have byte-based capacity budgets; Stations have airtime-based capacity budgets. Keep local-account service, transit relay, and network/system measurements distinct. Mail manifests/control consume the relevant Band 2 account or relay airtime share, without automatically debiting user payload-byte quotas. Attributable overhead consumes Station time. Receiving, forwarding, setup, ACKs, and retries must be measured where supported, attributing occupied intervals once in a Station ledger.

Transit forwarding does not debit a local user's byte allowance merely because that Station handles it. Internet-only transfers consume no HF airtime. Passive listening is not transmitting channel occupation, although radio availability is a separate scheduling constraint. Unknown metrics remain unknown or explicitly estimated.

Emergency overrides ordinary budgets; other eligibility, permission, holds, and capacity-tier restrictions still apply. Whether local-account manifests continue after the broader local-service Station allowance is exhausted remains a separate policy boundary, not answered by the configurable per-lease control cap.

Existing Server accounting authority, no paid ordinary precedence, transport-owned ARQ/stores, privacy gates, and Phase 5 authorization requirements remain unchanged. [ADR-007](ADR-007-hf-link-capacity-tiers-and-survival-mode.md), merged through [Project PR #35](https://github.com/OceanMail/oceanmail-project-archive/pull/35), defines the separate HF capacity tiers. Those tiers govern eligibility within this scheduling structure; ADR-008 does not change their thresholds.

## Implementation acceptance

Station issue #22 remains open. Required evidence includes:

- correct Bands 0–3 classification, including Emergency control in Band 0, public coordination in Band 1, ordinary manifests/receipts/control and local/relay payload in Band 2, and background broadcasts in Band 3;
- full-lease necessary route establishment, yielding at expiry, progress/backoff across failed attempts, and return to the normal Band 1 cap;
- Band 2 receiving unused Band 1 time, no Band 3 reservation, and early channel release when work ends;
- authenticated Server promotion into Band 1 without the route exception or sender-controlled priority;
- local-account and relay-peer fairness, bounded acceptance/backlog, and durable accounting across reconnect/restart;
- announcements, negotiated same-channel control/payload, optional shared broadcasts, and validated overhearing without custody or disclosure bypass;
- bounded single-radio Emergency discovery/preemption and coordinated access, demonstrated rather than assumed;
- transport-safe bounded batches/resume, essential ACK handling, truthful overhead accounting, and degraded-link eligibility.

No scheduler implementation, collision-free protocol, runtime/RF validation, or production security readiness is claimed by this documentation. Numeric lease/cap tuning, fairness weights, batch/listening durations, and broadcast cadence remain subject to testing.
