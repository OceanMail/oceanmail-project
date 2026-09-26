# ADR-002 — HERMES/Mercury Upstream-First Communications Foundation

- Status: ACCEPTED
- Original program decision: 2026-09-03
- Centralized here: 2026-09-11
- Preserves: Desktop Decision 0003 and the 0.1-to-0.2 transition decision

## Context

OceanMail 0.1 planned a clean-sheet communications stack centered on BEMPIC and M4P. Investigation showed that Rhizomatica HERMES/Mercury already provides substantial constrained-link store/transport, modem, radio, and test foundations.

## Decision

OceanMail 0.2 is HERMES-derived/upstream-first rather than a clean-sheet HF stack.

Initial baseline:

```text
OceanMail client
    -> OceanMail Station
    -> HERMES UUCP/uucpd/uuxcomp
    -> Mercury
    -> constrained link
```

Additional transports may be integrated behind the Station boundary.

Permanent downstream forks require a concrete requirement that cannot reasonably be satisfied upstream. OceanMail-specific adapters, policy, evidence translation, and management remain OceanMail responsibilities.

BEMPIC remains frozen and M4P integration remains tabled until comparative/field evidence establishes material value or a missing capability.

## M4P and GRID / CONTROL boundary

M4P remains useful prior art, not a current implementation layer. Its knowledge-driven state dissemination, typed DataLink evidence, peer-receipt separation, and silent-link scheduling work may inform later OceanMail design. They must not be inserted into the HERMES/Mercury/Taylor UUCP path merely because they address similar problems.

HERMES/Mercury supplies the current STORE / TRANSPORT baseline; it does not by itself solve OceanMail's future independently administered identity, federation, service/gateway discovery, relay selection, reputation, or opportunistic-routing requirements. Those concerns belong to the evidence-gated GRID / CONTROL plane above the transport boundary.

Any proposal to activate M4P must be a new deliberate architecture decision supported by an accessible implementation, an acceptable interoperability/federation model for the proposed scope, and comparative RF/field evidence showing a material advantage or missing capability. Specification activity alone is not sufficient.

## Consequences

- real store-forward email and measured behavior precede new protocol development;
- BEMPIC/M4P documents are historical/research authority only;
- M4P algorithms may be cited as design inputs without making OceanMail an M4P implementation;
- OceanMail does not add a second fragment, retransmission, receipt, or scheduling system over HERMES/Mercury/Taylor UUCP;
- multi-hop networking is evidence-gated;
- exact upstream pins and integration deltas remain component-local Station implementation truth.