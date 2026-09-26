# HERMES / Mercury Integration Workstream

## Purpose

Use and validate upstream HERMES/Mercury communications capabilities as OceanMail 0.2's constrained-link foundation without creating an unnecessary permanent downstream fork.

## Primary repository

`OceanMail/oceanmail-station`

## Current state

The Station repository contains the active pins, laboratory harnesses, Phase 0–4I evidence, and one explicitly tracked laboratory HERMES patch for reciprocal-session behavior. Exact versions and patch provenance are component-local Station truth.

The HERMES mail-compression laboratory also pins `spmfilter/libcmime` 0.2.2 at commit `dd21eb096d162656e30243f60fc4bc35ad39ae6e` and currently applies a small build-time source compatibility edit. Station `docs/UPSTREAM_BASELINE.md` is authoritative for that dependency/delta; it must be removed or converted to an explicit reviewed patch/rationale when the pin or publication/distribution boundary is revisited.

The proven no-radio path includes standard mail, Postfix, HERMES compression/UUCP integration, Taylor UUCP, Mercury simulated constrained transport, remote mailbox receipt evidence, and returned receipt correlation.

Phase 4I proved a specific reciprocal-session defect in the pinned HERMES VARA/Mercury data bridge: retired UUCP tail bytes could survive the old session and appear as `OOOOOO` where the next Taylor slave greeting should be `Shere`. The accepted OceanMail laboratory patch drains that retired TCP tail at the old-session cleanup boundary and adds an explicit cleanup-complete boundary. `Rhizomatica/hermes-net/main` was rechecked on 2026-09-11 and still lacks this fix. Station upstream lifecycle work tracks the focused upstream report/PR; do not silently remove the local patch or weaken the reciprocal-session gates until an upstream replacement is accepted and the full acceptance is rerun.

## Upstream relationship and collaboration state

On 2026-09-08, Rhizomatica maintainer Rafael Diniz responded directly to OceanMail's upstream inquiry and:

- invited OceanMail to contribute generally useful changes through upstream pull requests and issues;
- confirmed that maritime/mobile operation is of interest to HERMES;
- specifically identified automatic gateway selection as a capability HERMES wants;
- indicated interest in discussing/co-developing future solutions rather than having OceanMail independently build a parallel stack;
- confirmed that `Rhizomatica/hermes-frontend` is the next-generation frontend under development and that Rhizomatica intends its code to be GPL-covered.

This is an upstream-collaboration opportunity, not authority to assume that proposed OceanMail behavior is already accepted HERMES architecture. Features remain OceanMail-specific until their boundary is agreed upstream or implemented in OceanMail under the normal project decision process.

Preferred technical collaboration is asynchronous and written through focused GitHub issues/pull requests and email so architecture questions, code references, and decisions remain durable. A live technical call is not a project dependency.

## Relevant upstream UI/API transition

At the time of the upstream exchange:

- `Rhizomatica/hermes-gui` is the established Angular HERMES station GUI;
- `Rhizomatica/hermes-frontend` is a newer Next.js/React frontend monorepo consuming `Rhizomatica/hermes-api` and is still under development.

OceanMail should treat the future backend/frontend relationship as an upstream question rather than infer a long-term canonical architecture from repository names alone.

## Policy

- upstream first;
- exact accepted pins;
- explicit, narrow, auditable downstream deltas;
- preserve upstream licenses;
- contribute upstream where practical;
- do not vendor/fork implementation merely for convenience.

## M4P reference assessment

M4P is not part of the active OceanMail 0.2 stack. The former mandatory `OceanMail -> BEMPIC -> M4P -> DataLink` architecture is superseded, and later upstream M4P progress does not displace the proven HERMES/Mercury/Taylor UUCP baseline.

Useful M4P design inputs for later OceanMail work include:

- knowledge-driven dissemination, freshness, spacing, and redundant-advertisement suppression for possible GRID / CONTROL state;
- a typed link contract in which adapters report medium facts such as endpoint sets, collision domains, send outcomes, delivery confirmation, and payload-budget opportunities while higher layers own belief and policy;
- strict evidence separation: link acceptance (`sent`) is not peer delivery, peer receipt is not far-side mailbox acceptance, and none of those is human-read proof;
- the principle that prolonged silence must not deadlock future link attempts.

Two M4P ideas remain **unresolved OceanMail candidates**, not accepted behavior:

- origin-authored permitted-transport constraints that intermediates may narrow but never widen;
- adapting silent-link scheduling fallback to future Station rendezvous/call policy.

M4P fragment spacing, transmission receipts, and retransmission machinery are not to be duplicated above Mercury/HERMES/UUCP. Mercury and the connected link own modem/ARQ behavior; Taylor UUCP and the mail path own durable multi-day work and interruption recovery; Station correlates policy and evidence around those authoritative stores.

### Requirements not supplied by the active lower-layer baseline

HERMES/Mercury does not itself define OceanMail's future open-network identity, independently administered trust/federation, service and gateway discovery, relay selection, reputation, or opportunistic multi-hop policy. These remain GRID / CONTROL questions, and global multi-hop remains deferred until measured need justifies it.

M4P does not currently remove those questions for OceanMail. Its public specification uses persistent global UIDs mapped to compact deployment-local 8/16-bit addresses inside a static `network_id`; it describes network coordination rather than a global routing protocol. Cross-`network_id` federation, independently verifiable public identity/admission, rolling wire-protocol evolution, and application Message Type coordination are not defined for OceanMail's prospective public-network scope. Its approximately 7.4-hour maximum packet TTL is also a poor fit for some multi-day maritime contacts, while the current UUCP baseline naturally retains durable work longer.

### Historical public-network requirements retained for evaluation

The OMGP-era concept remains requirements evidence, not a current implementation plan. If broader GRID / CONTROL scope is reopened, evaluate whether a proposal can support independently administered vessels, shore stations, buoys, relays, and autonomous systems that encounter one another without shared advance provisioning; operate across radio, connected HF, acoustic, IP, or multiple modalities; retain useful work through multi-day contact gaps; coexist across upgrade schedules; discover suitable services/gateways rather than require one fixed destination; age stale reachability quickly and suppress redundant signaling; and preserve very low constrained-link overhead. This does not authorize speculative worldwide mesh implementation before the project's evidence gate is met.

A two-level federation model remains a candidate, not a decision: persistent cryptographically derived global identity for discovery/trust plus compact temporary aliases within a neighborhood, realm, or contact session. Any future scope translation must preserve original source/message identity, deduplication, and security context rather than merely rewrite a short address; no OceanMail identity, address, discovery, or wire format has been selected.

### Verified upstream snapshot

As checked on 2026-09-11:

- M4P specification `main` includes the merged knowledge-driven forwarding/DataLink/receipt work at `2eca9e8`; release `v0.3` predates that merge.
- [PR #3](https://github.com/Poseidons-Forge/m4p-spec/pull/3), the no-wire-change silent-link scheduling fallback, remains open.
- The public specification is CC BY 4.0. Its README describes the separate software implementation as Apache 2.0; M4P is not AGPL. The referenced `m4p-rs` implementation was not publicly accessible for independent inspection.
- OceanMail's broader design feedback was posted in the maintainer-requested [OceanSoft forum thread](https://forum.oceansoft.org/t/introducing-m4p-an-open-protocol-for-delay-tolerant-maritime-mesh-networking/46/3).

Revalidate all upstream state, licenses, releases, and implementation availability before any future dependency decision.

## Outstanding work

- upstream the proven Phase 4I reciprocal-session stale-TCP-tail/lifecycle fix tracked in `OceanMail/oceanmail-station#35`, including the `OOOOOO` versus `Shere` reproduction and accepted old-session cleanup-boundary rationale;
- establish the written upstream technical thread and, where useful, open focused issues covering:
  - future HERMES API/backend/frontend boundaries versus the existing email/UUCP stack;
  - automatic peer/gateway discovery and selection;
  - mobile stations that frequently appear/disappear and short/asymmetric contact windows;
  - whether store-carry-forward and any future multi-hop behavior belongs upstream or in an OceanMail-specific layer;
  - the boundary between generally useful HERMES functionality and OceanMail maritime/product policy;
- ask upstream to add explicit license files/SPDX metadata where repositories such as `hermes-frontend` do not yet make exact redistribution terms self-contained in Git;
- security/account/API work before broader LAN/product exposure;
- later physical-radio validation;
- measure other transports where justified;
- design GRID / CONTROL identity, federation, service/gateway discovery, and relay policy only in bounded evidence-gated phases;
- resolve end-to-end permitted-transport and silent-link attempt semantics before implementation;
- revisit BEMPIC, M4P, or multi-hop layers only if measured baseline limitations justify added complexity and the ADR-002 evaluation gate is satisfied.
