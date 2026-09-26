# Initial BEMPIC M0 Implementation Thread — Disposition

Status: HISTORICAL / RECONCILED 2026-09-11

## Scope and repository identity

This record closes the original OceanMail implementation thread that began against `OceanMail/oceanmail-desktop` and coordinated read-only with separate BEMPIC work. After the organization migration, that source history is preserved as [`OceanMail/oceanmail-0.1-prototype`](https://github.com/OceanMail/oceanmail-0.1-prototype); the related research repositories are [`OceanMail/bempic`](https://github.com/OceanMail/bempic) and [`OceanMail/bempic-reference`](https://github.com/OceanMail/bempic-reference).

This document is historical orientation, not current implementation authority. Current architecture is defined by the project spine and the active component repositories.

## What the thread established

The thread first accepted the OceanMail 0.1 clean-sheet path:

```text
OceanMail -> BEMPIC -> M4P -> DataLink
```

It then:

- reconciled stale 0.1 documents so M4P, not BEMPIC, owned generic routing, store-carry-forward, network deduplication, TTL, and network fragmentation;
- kept OceanMail responsible for application/mail semantics and consumer requirements while BEMPIC retained authority over its encoding, synchronization state, persistence/resume semantics, receipts, and conformance;
- created a small Rust workspace and cross-platform CI for the OceanMail application model, laboratory fixture, integration boundary, and accounting types;
- aligned the historical text-email model with one-or-more recipients, optional subject, explicit creation/ordering input, and stable application identity rather than treating the initial single-recipient fixture as the complete domain model;
- retained an exact synthetic RFC 5322/MIME fixture at `tests/fixtures/m0-original.eml`; that fixture is 330 bytes and exists to separate application normalization from later protocol/transport measurements; and
- required deterministic measurements for application/semantic bytes, protocol traffic by direction, carrier/link bytes when observable, useful committed bytes, duplicate/retransmitted payload, quote error, and elapsed simulated time.

The exact historical M0 decision and consumer contract remain on the `archive/v0.1-generation` branch of `oceanmail-0.1-prototype`, especially:

- `docs/adr/0001-layer-boundary-and-m0.md`;
- `docs/BEMPIC-INTEGRATION-REQUIREMENTS.md`; and
- `crates/oceanmail-sync/src/lib.rs`.

Later 0.1 work added stronger application identity, normalization, conflict, receipt, planner, and BEMPIC research evidence. Those repository artifacts supersede intermediate chat statements that BEMPIC Reference was nonexistent, unlicensed, or only a Python proof.

## Evidence boundary

At the final OceanMail checkpoint in this thread, commit `d8987eac38a3f5bea7ca95e170847a6f7d5991ad`, `oceanmail-lab` prepared the canonical fixture and printed its 330-byte source baseline but explicitly reported that no BEMPIC transfer was attempted.

The BEMPIC repositories later produced separate Python and Rust interruption/resume, simulator, vector, and conformance research evidence. That work does not retroactively turn the OceanMail M0 checkpoint into an integrated end-to-end proof, a released BEMPIC wire format, or current OceanMail 0.2 product evidence.

The 330-byte value is only the size of that exact synthetic source message. It is not:

- a typical-email-size claim;
- a HERMES `uuxcomp` baseline;
- a Mercury/link-byte measurement;
- a BEMPIC savings claim; or
- a production efficiency target.

## Retained test lessons

Two lessons remain applicable when current Station/HERMES/Mercury work compares constrained-link behavior:

1. Faults must be injected at the layer being tested. A reliable ordered or ARQ-style carrier may be bandwidth-limited, delayed, and disconnected/reconnected, but random missing bytes must not be presented as behavior of that same reliable stream. Loss/corruption testing requires an explicitly named lower-layer or unreliable-carrier profile.
2. Accounting domains must remain separate. Source/application bytes, normalized or compressed payload, protocol control traffic, carrier bytes, physical/link bytes, duplicates/retransmissions, elapsed time, and delivery/receipt evidence must not be collapsed into one efficiency number.

These lessons do not assign current implementation responsibility to BEMPIC or M4P and do not authorize duplicating Mercury/HERMES ARQ, retransmission, UUCP, or store/transport behavior in OceanMail.

## Superseded and intentionally not carried forward

The following thread positions are obsolete as current project direction:

- BEMPIC/M4P as mandatory OceanMail layers;
- completion of BEMPIC M0 as the next OceanMail communications milestone;
- waiting for a BEMPIC package/API as an active OceanMail blocker;
- the provisional M4P-replaceable network port as current implementation work;
- assumptions that BEMPIC Reference lacked a license or substantial Rust implementation; and
- active M4P middleware-release tracking as a reason to delay HERMES/Mercury work.

On 2026-09-02/03 OceanMail 0.2 moved to the upstream-first HERMES/Mercury/Taylor UUCP baseline, froze BEMPIC, and tabled M4P. BEMPIC may resume only after equivalent-condition comparison against the measured HERMES baseline demonstrates material value worth the additional protocol and maintenance burden.

See [OceanMail 0.1 → 0.2 Transition](0.1-to-0.2-transition.md) for the controlling generation change.
