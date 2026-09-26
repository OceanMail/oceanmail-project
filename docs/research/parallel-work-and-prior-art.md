# Parallel Work and Prior Art

Status: **CURRENT research index; not implementation authority for third-party capabilities**

## Purpose

Record products, protocols, software, standards, and historical systems that overlap OceanMail's goals so useful prior art is not lost when old conversations or prototype repositories are retired.

This file deliberately carries forward the useful research from the frozen 0.1 `GREAT_PARALLEL_WORK.md` while reconciling it to current OceanMail 0.2 architecture.

Classifications used here:

- **Adopt / depend on** — current baseline or direct dependency direction.
- **Potential transport / interoperate** — may be supported where technically and legally appropriate.
- **Borrow / study** — useful design prior art; no dependency implied.
- **Historical / superseded** — worth remembering specifically to avoid reintroducing old architecture.

Exact third-party versions, licenses, APIs, modem commands, and feature claims must be revalidated against current upstream sources before implementation. Station-local accepted pins remain authoritative for HERMES/Mercury.

Patent-specific HF engineering constraints are tracked separately in [`patent-risk-and-design-around-register.md`](patent-risk-and-design-around-register.md). Review that register before implementing rendezvous, automatic channel selection, ALE-adjacent behavior, multi-hop relay, propagation-driven frequency selection, or Emergency RF access/relay mechanisms.

## Research and reuse rule

Before building a major subsystem:

1. search for established standards/software that already solve the constrained-connectivity problem;
2. prefer upstream contribution/interoperation to unnecessary clean-sheet reinvention;
3. borrow proven behavior where licensing and architecture permit;
4. separate useful algorithms from obsolete trust/security assumptions;
5. do **not** prefer a newer networking pattern merely because it is newer; intermittent/low-bandwidth historical systems deserve equal or greater consideration when their constraints match OceanMail;
6. choose modern alternatives when they provide a concrete advantage in security, interoperability, maintainability, hardware support, licensing, correctness, or measured performance.

---

# Current communications baseline

## HERMES / Taylor UUCP

**Role: Adopt / depend on.**

Current OceanMail 0.2 Station store/transport baseline. The active Station has already proven standard mail -> Postfix -> HERMES compression/UUCP integration -> Taylor UUCP -> Mercury simulated constrained transport -> remote mailbox -> returned receipt.

Relevant inherited strengths include durable spooling, asynchronous job transfer, unattended operation, retry, batching/compression, and separation of application mail behavior from intermittent link execution.

Exact integration pins and downstream laboratory deltas are Station-local authority.

## Mercury

**Role: Adopt / depend on; preferred open HF modem baseline.**

Current Station proof uses pinned Mercury. It provides the accepted modem/TNC boundary for the no-radio HERMES path and is the first modem to validate before OceanMail considers building lower-layer replacements.

Evaluate future radio, broadcast, link-quality, and control capabilities against current upstream Mercury documentation/code rather than historical chat claims.

## Hamlib / CAT radio control

**Role: Potential integration dependency / borrow.**

Radio tuning/PTT/frequency selection can be owned by Station/upstream radio-control software rather than by OceanMail application logic or a bespoke waveform. This is relevant to the legal-channel catalog and rendezvous -> working-channel research in Station.

---

# HF modem/link alternatives and adjacent radio technology

## PACTOR / SCS

**Role: Potential transport / interoperate.**

Mature adaptive HF ARQ with a substantial maritime/SailMail installed base. OceanMail should treat PACTOR reliability/adaptation as lower-layer behavior rather than placing another fine-grained ARQ protocol above it.

## SCS P4dragon / PXdragon and 2G ALE

**Role: Borrow / study / possible high-end integration.**

Important prior art for configured legal channel sets, unattended scanning, Link Quality Analysis, channel ranking, peer calling, automatic radio retuning, and trying alternate channels when establishment fails.

The implementation is proprietary; study behavior, do not assume reusable code or unverified current commands.

## Automatic Link Establishment (ALE)

**Role: Borrow / study.**

Established HF practice for scanning authorized channels, sounding/link-quality analysis, selecting a useful channel, calling a peer, and establishing a working link. Strong prior art for OceanMail's rendezvous-set -> working-channel concept.

## VARA HF

**Role: Potential transport / interoperate.**

Widely used software HF modem with adaptive connected ARQ. Surrounding host software may own CAT/radio/channel policy. Do not duplicate VARA's own link repair above it.

## ARDOP

**Role: Potential transport / borrow / study.**

Open HF modem/protocol family relevant to both connected ARQ and connectionless FEC/broadcast research. Useful for comparing pairwise reliable transfer against cooperative one-to-many behavior.

## HERMES Broadcast / RaptorQ

**Role: Borrow / study; upstream-first broadcast candidate.**

Relevant to one-to-many/data-carousel transfer where multiple Stations can benefit without each receiver participating in pairwise ARQ. Evaluate this before inventing an OceanMail fountain/erasure-code implementation.

## FreeDATA

**Role: Borrow / study.**

Open HF communications/modem/application project using FreeDV/Codec2 technology, useful as prior art for APIs, messaging/file transfer, broadcast experiments, and open modem architecture. Recheck current project health before relying on it.

## FreeDV / Codec2

**Role: Borrow / study lower-layer technology.**

Open modem/codec building blocks used by multiple HF projects. Useful background before contemplating any new OceanMail-specific modem or waveform.

---

# Existing maritime/radio-mail ecosystems

## Winlink

**Role: Interoperate / major prior art.**

Important established constrained-mail ecosystem spanning HF modems, RMS gateways, store/forward, forms, and radio-only/hybrid operation.

Any integration must use supported interfaces and respect applicable service/radio rules; native OMail must not be implemented by merely relabeling Winlink behavior.

## Winlink B2F

**Role: Borrow / study / possible interoperability.**

Useful prior art for low-bandwidth mail forwarding, batching, compression, attachments, and independent compatible clients.

## Winlink Express

**Role: Product/UX reference.**

Reference for integrated modem/radio-mail workflows, while OceanMail aims for a more unified cross-platform experience.

## Pat

**Role: Borrow / study / interoperability reference.**

Open-source Winlink client and useful prior art for B2F/client/session/modem integration. Revalidate current licensing/dependencies before reuse.

## Winlink RMS / RMS Relay / Hybrid / Linux gateway patterns

**Role: Borrow / study infrastructure patterns.**

Relevant to radio-to-network bridging, gateway/store-forward behavior, and external-network egress.

## SailMail

**Role: Potential integration/partnership; offshore-market reference.**

Major maritime PACTOR email service. Do not assume its transfer interface is open or third-party use is permitted; any integration requires explicit technical/service/legal validation.

## AirMail

**Role: Product/interoperability reference.**

Established maritime radio-email client workflow relevant to SailMail/Winlink users and existing onboard practices.

---

# Historical intermittent-mail and BBS architecture

## UUCP / rmail / Batch SMTP

**Role: Major prior art; partially embodied in current baseline.**

Core lesson: the application remains useful while disconnected; connectivity is an opportunity to exchange durable queued work.

Useful ideas:

- durable local spool;
- unattended calls/sessions;
- batch exchange;
- retry/backoff;
- destination-oriented queued jobs;
- application/link-scheduler separation;
- forwarding through intermediates where justified;
- asynchronous serialized application transactions (for example Batch SMTP over UUCP, RFC 976).

Do not copy topology-dependent bang-path user addressing.

## CSNET PhoneNet / MMDF

**Role: Major historical prior art.**

Intermittently connected institutions pushed/pulled queued mail through continuously available relays. MMDF's separation of mail handling from communications channels is directly relevant to OceanMail's client/Station/store-transport separation.

## FidoNet, FrontDoor, BinkleyTerm, Echomail

**Role: Major BBS/store-forward prior art.**

Useful ideas include:

- mailer process separate from user-facing application;
- unattended node-to-node exchange;
- destination-oriented packet batching;
- event/scheduling management;
- `Crash`/normal/hold-like urgency semantics as historical scheduling ideas;
- scanner/tosser separation;
- compact transfer representation separate from local message storage;
- retry/backoff behavior;
- `SEEN-BY` / `PATH` prior art for loop/duplicate suppression.

Do not copy topology-encoded addresses, unbounded route headers, or old trust assumptions.

## POP2

**Role: Historical mail retrieval prior art.**

Relevant behavior includes advertising message size before retrieval and separating successful receive/keep, successful receive/delete, and failure outcomes. Strong precedent for manifest-first cost awareness and not treating transfer success as immediate destructive deletion.

## SMTP / RFC 822 era mail

**Role: Interoperability foundation and useful contrast.**

SMTP standardized Internet mail but assumes a live reliable session far more than OceanMail may assume across constrained links. Preserve Internet interoperability at boundaries without requiring live end-to-end SMTP over the Grid.

## Kermit

**Role: Major historical transfer-protocol prior art.**

Relevant concepts:

- sliding windows;
- selective retransmission;
- negotiable/adaptive packet lengths;
- long packets on clean links and smaller packets on poor links;
- timeout adaptation;
- compression;
- capability negotiation.

Do not recreate fine-grained ARQ above Mercury/PACTOR/VARA/ARDOP when the modem already owns it. Apply the principle at appropriate logical synchronization/resume/broadcast boundaries or in future modem research.

## XMODEM / SEAlink

**Role: Historical transfer-protocol prior art.**

Useful mainly as the progression from simple stop-and-wait blocks toward windowed transfer and better restart/synchronization behavior.

## ZMODEM

**Role: Historical transfer-protocol prior art.**

Important lesson: continuously stream useful data when the path permits, while retaining restart/resume. At OceanMail's application level, useful progress must survive loss of the opportunity before a higher-level receipt returns.

## QWK / Blue Wave offline-reader packets

**Role: Major offline synchronization/UX prior art.**

Useful ideas:

- batch many small logical items;
- amortize framing/header costs;
- compress synchronization batches;
- keep manifests/indexes separate from message bodies;
- make a received synchronization artifact useful even if the link immediately disappears;
- read/compose/reply completely offline.

Do not copy historical fixed-field limitations.

## CompuServe TAPCIS / NavCIS / Navigator / AutoSig

**Role: Historical application-management prior art.**

Clients for expensive metered connections prepared work offline, automated logon/session task lists, uploaded already-composed material, downloaded new material, then disconnected quickly. Strong model for OceanMail's autonomous Station synchronization behavior.

## CompuServe B / B+

**Role: Historical transfer-protocol prior art.**

Purpose-built service transfer protocols that evolved toward larger packets/windowing. Useful lesson: optimize transport behavior around the actual application workload rather than generic interactive-terminal assumptions.

## Quantum Link / AOL

**Role: Historical constrained-link client/server and UX prior art.**

Useful ideas:

- hide modem/network complexity behind a simple integrated experience;
- keep presentation/assets local rather than retransmitting UI material;
- retain useful mail/content locally for offline operation (for example Personal Filing Cabinet concepts).

OceanMail should transmit semantic state/content, not presentation the client already knows how to render.

## Prodigy / NAPLPS

**Role: Historical constrained-link client/server prior art.**

Useful principle: stage reusable client code/assets locally and send compact changing semantic state over the slow link.

## Store-and-forward Usenet feeds

**Role: Historical batching/compression prior art.**

Useful for studying batch feeds, compression, asynchronous exchange, duplicate suppression, and the economics of scarce dial-up transfer windows.

---

# Delay/disruption-tolerant networking prior art

## Bundle Protocol v7 / ION-DTN / LTP / CFDP

**Role: Borrow / study.**

Useful concepts include disruption tolerance, explicit lifetime, persistent objects, delivery/status reports, interrupted transfer recovery, byte-range/file recovery, and extreme-latency operation.

OceanMail should borrow proven semantics where useful without assuming BPv7 must become its wire format.

## PRoPHET

**Role: Borrow / study; routing implementation remains evidence-gated.**

Uses encounter history, aging, and transitivity to estimate delivery usefulness instead of blindly flooding copies. Relevant to future Station relay relevance and destination/contact prediction.

## Spray-and-Wait

**Role: Borrow / study bounded replication.**

Limits active copies in intermittently connected networks rather than using epidemic replication. Strong prior art for bounded primary/secondary responsibility and passive-shadow-copy research.

## Reticulum

**Role: Borrow / study; not selected as current OceanMail network layer.**

Useful prior art for decentralized identities, announcements, path requests, hop-aware state, heterogeneous interfaces, and bounded discovery traffic.

## DTN7

**Role: Borrow / study software modularity.**

Useful daemon/API/pluggable-link architecture prior art.

## LXMF

**Role: Borrow / study future low-bandwidth messaging/chat.**

Asynchronous messaging over Reticulum; useful for future OChat/offline UX research.

## Briar

**Role: UX/offline-messaging influence.**

Useful reference for messaging that can survive changing Internet/local/offline connectivity without making network details the user's concern.

## Meshtastic / LoRa and other off-grid meshes

**Role: Borrow / study.**

Useful for compact discovery, low-power operation, store-forward, broadcast suppression, and mobile/offline UX. They are not current OceanMail's communications foundation.

---

# Other adjacent product/service work

## OpenSail and offshore weather/routing tools

**Role: Potential future integration / influence.**

Reference for bandwidth-budgeted offshore weather/routing workflows. Prefer integrating specialist forecasting/routing services rather than building an unnecessary forecasting operation.

## Mailcow and conventional Internet mail infrastructure

**Role: Hosted-service/infrastructure reference, not constrained-link architecture.**

Use established SMTP/IMAP/mail-server components where they fit rather than rebuilding commodity Internet mail behavior.

## Gmail / Outlook / Yahoo / conventional IMAP-SMTP providers

**Role: Future interoperability/integration.**

Provider integration belongs at supported client/Server adapter boundaries and must respect provider authentication/APIs; it does not redefine native OMail transport.

---

# Historical OceanMail-specific work

## BEMPIC

**Role: Historical / frozen research.**

Valuable research into compact/interruption-tolerant application synchronization, but frozen 2026-09-02 and not an active mandatory 0.2 layer.

## M4P

**Role: Historical / tabled for OceanMail 0.2.**

Prior work on multi-modal mesh/store-carry-forward remains useful research evidence, but current OceanMail does not adopt M4P on the active critical path. Revisit only if comparative/field evidence justifies the added layer.

## Old mandatory `OceanMail -> BEMPIC -> M4P -> DataLink` stack

**Role: Superseded.**

Do not restore this architecture merely because historical documents describe it. Current HERMES/Mercury upstream-first decisions control.