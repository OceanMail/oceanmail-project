# OceanMail Communications Foundation Positioning

Status: ACTIVE PROJECT POSITIONING

This document records the durable boundary conclusions from the HERMES/Mercury evaluation that are not implementation-pin details.

## OceanMail versus HERMES

For the narrow problem "move ordinary email between a vessel and an HF/shore gateway," HERMES already provides much of the communications plumbing OceanMail 0.1 expected to build itself. OceanMail 0.2 therefore does not compete by recreating modem DSP, generic ARQ/FEC, UUCP store/forward behavior, radio-control internals, compression, or related lower-layer machinery when maintained upstream components satisfy the requirement.

OceanMail remains distinct where it adds maritime product and service behavior above that foundation, including:

- vessel, crew, user, account, and device experience;
- autonomous OceanMail Station policy, persistence, authorization, evidence, and accounting;
- OceanMail Desktop and future client UX;
- hosted OceanMail service behavior and conventional Internet-mail handoff;
- continuity across constrained links and ordinary IP transports;
- interoperability with external maritime/radio-email systems where authorized;
- later evidence-gated gateway discovery, relay, and opportunistic networking behavior.

If OceanMail were reduced to only direct HF email-to-gateway plumbing, much of that implementation would be redundant with HERMES. OceanMail engineering effort should therefore remain concentrated on capabilities that are genuinely OceanMail-specific or on generally useful upstream contributions.

## Rhizomatica repository/fork rule

Do not fork the Rhizomatica organization wholesale.

Evaluate upstream repositories independently as one of:

1. current direct dependency;
2. deferred but strategically relevant upstream candidate;
3. research/prior art;
4. vendor/upstream mirror or otherwise not owned by OceanMail.

Permanent downstream forks require a concrete need that cannot reasonably be satisfied upstream. Prefer small, explicit, source-pinned integration deltas and upstream contribution over private divergence.

Current component-local pins, accepted patches, exact licenses, and reproducibility evidence remain authoritative in `OceanMail/oceanmail-station/docs/UPSTREAM_BASELINE.md`.

Strategically relevant upstream capabilities include HERMES Broadcast/RaptorQ for acknowledgement-poor/broadcast use, HERMES radio-daemon/Hamlib for later physical-radio control, and Skywave for comparative modem/channel testing. They are not automatically on the current critical path.

Visible source is not by itself permission to derive or redistribute it. Applicable license terms must be established before OceanMail incorporates, modifies, or distributes upstream code. The HERMES frontend/backend/GUI family is reference material unless a current need and suitable license boundary justify direct reuse.

## SailMail and Winlink positioning

SailMail and Winlink are important operational references and possible interoperability targets, not OceanMail's architectural foundation.

### SailMail

SailMail is highly relevant prior art and an existing operational solution for supported cruising yachts. Its current service rules limit membership to non-commercial vessels under 1,600 tons and impose service-specific operating terms. That makes SailMail valuable for maritime operations/UX comparison but not a general foundation for OceanMail's broader recreational/commercial product scope.

Official terms should be rechecked before any implementation or user-facing compatibility claim:

- https://sailmail.com/cost-and-application-process/terms-and-conditions/

### Winlink

Winlink is highly relevant prior art for global radio email, store/forward operations, and multi-modem integration. Public Winlink use over amateur radio is subject to amateur-radio content/privacy rules, including restrictions on business traffic and intentional message-content encryption. That makes the public amateur network unsuitable as OceanMail's general commercial/private maritime service foundation, even though Winlink technology and non-amateur authorized uses remain important references.

Official terms should be rechecked before implementation or user-facing compatibility claims:

- https://winlink.org/terms_conditions

### HERMES comparison

HERMES does not provide SailMail/Winlink's ready-made worldwide gateway footprint, but its open/adaptable technical foundation is better aligned with OceanMail's need to deploy and evolve its own mixed maritime environment subject to the applicable radio/service authorization.

## Development environment

Debian/Linux is the default OceanMail 0.2 integration-development environment for Station, HERMES/Mercury, UUCP, Hamlib/radio work, simulation, Server/backend integration, and Infrastructure work.

Windows remains required for Windows-specific Desktop behavior, packaging, and platform validation. This is a development preference, not a restriction on supported client platforms.

## Historical conclusions not carried forward as current facts

The following evaluation artifacts are intentionally not project truth:

- old point-in-time Mercury throughput/goodput numbers;
- numerical HERMES-versus-OceanMail scoring tables;
- speculative percentage estimates of work avoided;
- a proposed fixed BEMPIC reactivation threshold such as a specific percentage byte/airtime improvement;
- the abandoned idea of forking every Rhizomatica repository;
- the former mandatory `OceanMail -> BEMPIC -> M4P -> DataLink` stack.

Those were useful reasoning aids but are either time-sensitive, unmeasured, superseded, or too specific to preserve as architecture.