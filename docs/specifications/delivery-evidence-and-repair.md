# OMail Delivery Evidence and Repair

Status: **CURRENT cross-component semantics; relay/multi-hop execution remains deferred/evidence-gated**

## Purpose

Define what OceanMail may truthfully claim about message delivery and how it should recover when final evidence does not return, without treating a relay handoff as delivery or solving uncertainty by flooding duplicate payloads.

This specification is transport-independent. HERMES/Mercury/Taylor UUCP and later accepted transports execute store/transport work; OceanMail Station/Server/Desktop own the application-level identity, policy, evidence, and user-visible meaning described here.

This document does **not** authorize speculative global multi-hop routing. Current program policy still proves direct Station/gateway behavior first and requires measured need before multi-hop forwarding is implemented.

## Core evidence rule

A message is not delivered merely because it:

- left a local Postfix queue;
- entered a Taylor UUCP job;
- moved bytes over Mercury or another link;
- completed a caller/process session;
- was handed to an intermediate relay; or
- was accepted for future forwarding by another Station.

Sender-visible delivery confirmation requires returned evidence from an authoritative destination for the applicable delivery objective.

For native OMail this normally means durable destination mailbox/Station receipt evidence. For a hosted or external delivery objective, the strongest evidence available from the authoritative Server/gateway/external service must be reported without claiming more than that service proves.

Human reading is separate. A future read receipt, if supported, is an optional user-level feature and is not required for network delivery confirmation.

## Stable logical OMail identity

Every OMail message needs a durable logical identity that survives:

- transport retries;
- local queue-ID changes;
- lost sessions;
- relay handoffs;
- a later re-injection after an earlier dissemination attempt has expired; and
- delivery through a different accepted transport or path.

The current Available contract already requires an OceanMail logical message ID distinct from an RFC `Message-ID`. RFC `Message-ID` remains useful correlation evidence but is not, by itself, sufficient authorization or globally trustworthy identity.

A new transport/dissemination attempt may have a new attempt ID, job ID, lower-layer packet identity, route, transport, or lifetime while remaining the **same logical OMail message**. A retry must not create a second Inbox message merely because the transport attempt is new.

## Compact destination receipt

When an authoritative destination has validated and durably stored a complete message, it should be able to generate a compact, versioned, idempotent receipt tied to the logical OMail identity.

Production receipts require an accepted trust/authentication design. The current Phase 4I Station proof demonstrates returned receipt transport/correlation only at `lab_peer_transport_unverified`; it does not establish production cryptographic trust or human-read status.

Receipts and closely related repair/status records are high-value system/control microtraffic because a small amount of evidence can suppress retransmission of a much larger payload. Under [ADR-009](../decisions/ADR-009-personal-traffic-and-encryption.md), ordinary delivery receipts, custody evidence, repair/status records, stop-flow, and tombstones belong in Band 2 as expedited mail control, ahead of ordinary payload at safe transport boundaries. They consume the relevant Band 2 account/relay airtime share, not the Band 1 allowance. Emergency's own receipts, stop-flow, and tombstones remain in Band 0. This supersedes the original Band 1 placement and the earlier ordering that placed ordinary receipts below own-vessel payload; essential link-layer acknowledgements stay within the exchange they support.

## Source retention

The originating Station should retain sufficient recoverable source state/content until one of these occurs:

- adequate final delivery evidence is received;
- explicit retention/expiry policy ends automatic repair;
- the user intentionally cancels/abandons the message; or
- another accepted policy explicitly permits removal.

An intermediate handoff or relay responsibility acknowledgement is not, by itself, enough reason to destroy the source's only repair copy.

Source retention, relay-cache lifetime, responsibility lifetime, and compact delivery-record lifetime are separate policy values.

## Lost receipt does not mean failed delivery

OceanMail must assume that a destination or relay may disappear temporarily for ordinary reasons: power-down, propagation loss, maintenance, movement, battery conservation, hardware failure, or simply no useful return path.

Therefore absence of a final receipt is **unknown**, not automatically failed.

Repair timing should use patience/backoff based on available evidence such as:

- Emergency versus Ordinary class;
- message age;
- last useful destination/relay observation;
- current known replication/responsibility evidence;
- expected constrained-link latency;
- prior attempt state;
- Server/gateway verification opportunities; and
- whether a materially new path/opportunity has appeared.

Exact timers and thresholds are not frozen here.

## Probe before payload re-injection

When an earlier attempt appears stale or its ordinary transport/cache lifetime is likely to have expired without final evidence, OceanMail should normally seek compact status evidence before sending the full payload again.

Candidate probes, where authorized and useful, include:

1. local/peer synchronization state for the logical message ID and any returned receipt;
2. a known responsible relay/holder;
3. the destination Station/account when reachable;
4. OceanMail Server when it is authoritative for relevant hosted state; and
5. another authoritative gateway/service when that delivery objective exposes suitable evidence.

Three outcomes are distinct:

- **positive evidence** — suppress re-injection and update delivery state;
- **explicit negative evidence** — may justify a new bounded attempt;
- **no response / unknown** — use further patience, backoff, a materially new opportunity, or escalation policy rather than pretending either success or failure.

## Bounded re-injection

If another attempt is justified, re-inject the **same logical OMail message** under a new attempt/epoch rather than creating a semantically duplicate email.

A new attempt may legitimately use a different transport, gateway, responsible relay, or renewed lower-layer lifetime. Deduplication and destination presentation must still recognize it as the same logical message.

Automatic repair for Ordinary mail must be bounded. After repeated uncertainty/failure, further work should require longer backoff, a materially new opportunity, or user attention rather than endlessly generating traffic.

A truthful user-facing terminal state is `Delivery unconfirmed` / `Needs attention` rather than infinite hidden retries.

Emergency may use a more aggressive repair/escalation policy, subject to later abuse/authentication controls and applicable law.

## Long-lived delivery tombstones

A compact delivered-message record should normally be retainable much longer than a large relay payload.

Conceptually it records that logical message `M` reached the applicable authoritative destination, with enough trusted evidence/generation information to suppress stale re-injection.

This allows a Station to evict a large cached payload under ordinary retention/storage pressure while retaining a tiny fact that prevents an old source or stale relay from resurrecting already-delivered mail later.

Tombstones/receipts must themselves be bounded, deduplicated, privacy-aware, and synchronized only within authorized scopes.

## Future relay responsibility semantics

These requirements apply **if/when** relay/multi-hop behavior is implemented. They do not by themselves authorize that implementation.

### Responsibility is not final delivery

A relay may explicitly accept responsibility to attempt onward delivery. That acknowledgement raises delivery confidence but does not equal destination receipt.

Responsibility should be time/evidence bounded rather than permanent. A stale responsibility role may become eligible for replacement without requiring immediate deletion of the relay's stored copy.

### Bounded active copies

Do not use epidemic payload replication by default.

Future designs should distinguish:

- **active responsibility copies** — a bounded set of Stations selected/authorized to deliberately advance the message; and
- **passive/observed/shadow state** — information or opportunistic retained data that does not automatically gain the right to create more descendants.

A conceptual primary/secondary responsibility model is valid research, but the exact number of active copies is not frozen. Field evidence, Emergency handling, path diversity, storage pressure, and actual upstream transport capabilities must determine the final policy.

### Passive listeners do not become global caches

A Station that can decode traffic may learn inexpensive operational evidence—peer identity, link quality, object/receipt hints where lawfully/technically visible—without storing or propagating the payload.

Hearing a transmission loudly and clearly is not sufficient reason to retain it.

A Station in an unrelated region with no useful destination encounter history, gateway role, path diversity, or plausible movement toward the destination should normally ignore ordinary third-party payload rather than helping Hawaii-to-California traffic spread into caches around the planet.

Candidate relevance signals for future relay policy include:

- direct/recent contact with the destination;
- repeated encounter history;
- transitive encounter evidence;
- coarse geographic/ocean-basin relevance;
- vessel movement/heading where appropriately available;
- gateway/service reachability;
- historical relay success;
- path diversity; and
- number/quality/freshness of already known copies.

Geography is evidence, not an absolute prohibition: unusual HF propagation can create real long-distance opportunities.

### No second hidden routing protocol

Relay relevance, responsibility, and repair policy belong to OceanMail Grid/control semantics. Generic routing/forwarding must remain consistent with the selected transport/network architecture and the project decision that multi-hop complexity is evidence-gated.

Do not revive the old mandatory BEMPIC/M4P stack or implement an unreviewed parallel global router to satisfy this specification.

## Synchronization/manifests and repair evidence

Future constrained synchronization should be able, within authorization/privacy boundaries, to communicate enough evidence to answer questions such as:

- Is logical message `M` already known here?
- Is it complete or partial?
- Is final destination receipt known?
- Is a peer actively responsible for advancing it or merely observing/caching it?
- Is a retransmission likely to be redundant?

This does not require one giant global manifest and must not expose private Available metadata to unauthorized peers.

Progressive synchronization depth is desirable: a brief/weak opportunity should exchange only the highest-value compact state, while a stronger/longer opportunity may refine component, receipt, resume, or other permitted state. Exact levels and wire encoding remain future design work.

## Component responsibilities

### Desktop / clients

- present only evidence the Station/Server actually has;
- distinguish queued/transmitting/remote-received/delivery-unconfirmed from human-read status;
- do not manufacture delivery from local queue disappearance or elapsed time;
- surface user attention only after policy says automatic repair is exhausted or needs approval.

### Station

- correlate logical message identity with lower-layer jobs/attempts/evidence;
- preserve returned receipt and repair state durably;
- continue accepted work independently of clients;
- perform patient/bounded retry policy without duplicate payload queues when upstream stores already own the payload;
- if relay behavior is later implemented, enforce bounded responsibility/relevance rather than global flooding.

### Server

- answer delivery/status queries only where it is authoritative for the relevant hosted state;
- preserve distinction between Server acceptance, destination mailbox receipt, external-service evidence, and human reading;
- participate in production receipt trust/accounting only under accepted identity/security rules.

### HERMES / Mercury / UUCP / other transports

- provide their actual store/transport/link behavior and evidence;
- do not become the authority for OceanMail user-visible final-delivery semantics merely because a transport session succeeded.

## Non-goals / unresolved parameters

This specification does not freeze:

- receipt wire encoding or signature format;
- retry timers or maximum attempt counts;
- relay count/lease duration;
- global routing algorithms;
- final quota/billing treatment of retries/control records;
- a read-receipt feature;
- exact progressive-manifest levels; or
- physical-radio behavior before Phase 5 is authorized and tested.

Those decisions require implementation evidence, identity/security work, and/or field measurement.
