# Station Workstream

## Purpose

Provide the autonomous onboard/edge communications service for OceanMail 0.2.

## Repository

`OceanMail/oceanmail-station`

## Current architecture

- upstream-first HERMES/Mercury/Taylor UUCP store/transport integration;
- OceanMail-specific persistent state, policy, evidence correlation, management APIs, and Grid/control behavior;
- explicit logical separation between **STORE / TRANSPORT** execution/evidence and **GRID / CONTROL** network intelligence/policy; see `docs/decisions/ADR-004-station-store-transport-grid-control.md`;
- relay/gateway/OChat policy belongs to GRID / CONTROL; accepted work is executed through STORE / TRANSPORT rather than pushing OceanMail policy into upstream components;
- constrained-link scheduling uses the progressive capacity tiers and sub-0.1 kbps survival mode defined by `docs/decisions/ADR-007-hf-link-capacity-tiers-and-survival-mode.md`;
- no duplicate payload queues where Postfix/UUCP/mailbox/upstream components already own them;
- headless Linux service capable of serving multiple clients;
- strict evidence semantics and explicit production-security gates;
- vessel and permanent managed gateways run the same Station software; gateway is a role/configuration, not a separate product;
- native OMail remains decentralized and must not require central Server availability for viable boat-to-boat/store-carry-forward paths;
- gateway capability means exchanging eligible OMail traffic toward/from OceanMail Server when Internet is available, not acting as an independent public Internet SMTP server;
- Station may expose a local OMail/OChat/management Wi-Fi service network, but is not a NAT/general Internet router;
- routine abrupt power removal must be supported as normal marine operation with crash-safe automatic recovery.

Detailed deployment/power/networking requirements: `docs/specifications/station-deployment-power-networking.md`.

Cross-component constrained-link authentication/privacy requirements: `docs/specifications/constrained-link-authentication-privacy.md`.

Cross-component delivery confirmation, lost-receipt repair, stable logical identity, bounded reinjection, and future relay-copy-scope semantics: `docs/specifications/delivery-evidence-and-repair.md`.

Cross-component Grid accounting, Station metering, user approval, and Server-authoritative credit/service-policy semantics: `docs/specifications/grid-accounting-metering-and-service-policy.md`.

Current settled Grid-facing semantics include:

- no relay `Off` mode while a Station is running;
- Eager relays advertise; Reluctant relays remain silent and intervene only as fallback under accepted policy;
- gateway willingness is separate: Full / Minimal / Off for ordinary third-party service, with Emergency still eligible when technically capable and legally/operationally permitted;
- capacity tier primarily changes scheduler cost and eligibility: below 0.1 kbps, defer background/bulk work and normally avoid new ordinary relay payload while retaining bounded high-value relay opportunities; Emergency never bypasses technical or legal/operational authorization gates;
- Minimal Gateway fallback uses stranded/stalled Ordinary traffic and route/delay conditions, not a removed Priority class;
- OChat is ephemeral GRID / CONTROL behavior using shared transports, is not durable relay mail, and yields to OMail;
- an intermediate relay/store-forward handoff is not sender-visible final delivery; returned authoritative destination evidence controls that claim;
- Ordinary repair must tolerate delayed/missing return evidence and avoid unbounded duplicate payload replication;
- Internet gateway operation moves eligible OMail toward/from the centralized OceanMail public Internet-mail boundary defined by ADR-006; it does not make the Station an independent public SMTP server.

## Current implementation state

No-radio work is complete through Phase 4I, including returned receipt correlation. The Available/account-authorization/retrieval-plan foundation was accepted on 2026-09-11, alongside Debian trixie/Dovecot 2.4 compatibility and a real authenticated writable-IMAP `\Seen` state transition proof.

A nondeterministic Phase 4I readiness failure observed during Dovecot compatibility reconciliation passed on immediate rerun at the exact same source/head; the readiness race was corrected by bounded readiness-gate hardening and current-base integration validation without weakening the evidence contract.

The in-memory lease controller is supplemented by public
[Station PR #1](https://github.com/OceanMail/oceanmail-station/pull/1), merged on
2026-09-26: traffic classification, route-attempt backoff, Band 2 selection and a
deterministic no-radio harness, plus auth regression tests. These modules are
experimental and not connected to daemon transport dispatch. Restart-durable
accounting, capacity-tier integration, channel coordination and live validation
remain outstanding. See
[LEASE_CONTROLLER.md](https://github.com/OceanMail/oceanmail-station/blob/main/docs/LEASE_CONTROLLER.md).

Current follow-on work:

The merged laboratory implementation provides the first loopback-only Phase 4J
authentication slice. Production identity and LAN release remain gated.
Receipt trust remains laboratory-only. See
[`station-client-implementation-gates.md`](../docs/specifications/station-client-implementation-gates.md)
before proceeding from lab context to private Available/plan/accounting state.

- production authenticated permission-scoped API/account identity;
- account-scoped Available/retrieval/ledger API after production authentication;
- ADR-008 scheduler follow-on: implement Bands 0–3, Band 1 cap/route exception, Band 2 local/relay fairness, unreserved broadcasts, and negotiated/single-radio channel behavior within ADR-007's capacity tiers, survival behavior, and authorization gates. Track each remaining implementation slice in a public issue before assigning it;
- production encrypted storage/per-user key separation;
- Grid/control, relay/gateway, accounting/scheduling, API expansion;
- authenticated Station/Server gateway exchange consistent with ADR-006;
- hardware qualification for low-power ARM64 vessel Station and fanless x86-64 permanent-gateway reference profiles;
- Wi-Fi AP/client/failover qualification and repeated hard-power-loss recovery testing.

Physical-radio Phase 5 remains held pending authorization/hardware scope.

## Test and hardware planning

The component-local staged test/acquisition plan is [`OceanMail/oceanmail-station/docs/testing-hardware-acquisition-plan.md`](https://github.com/OceanMail/oceanmail-station/blob/main/docs/testing-hardware-acquisition-plan.md). It preserves the currently available development resources and intended validation progression:

- virtual/container hosts with independently isolated nodes for no-radio and failure-domain testing;
- repurposed Windows/Linux-capable laptops and older Intel Macs rather than purchasing dedicated mini-PCs for the current test program;
- controlled bench RF only after authorization, using two suitable USB-controllable HF transceivers plus correctly rated loading/attenuation/coupling equipment;
- later authorized local paths covering line-of-sight and obstructed links with representative fixed and marine antenna installations;
- later satellite/GPS/marine-electronics integration, regional participation and authorized moving-vessel trials.

The no-mini-PC decision applies to **development/test acquisition**, not the separate production/reference-hardware qualification requirements in `docs/specifications/station-deployment-power-networking.md`. The test plan is planning authority only; it does not authorize physical-radio Phase 5 or freeze a production hardware SKU.

## Deployment direction

The initial permanent Station is an owner-operated pilot; its specific location is private operational planning. Potential later institutional hosts include yacht clubs, university/maritime institutions, harbormasters, marinas, and similar sites. Wider hosted-gateway outreach is a future growth path after unattended operation is demonstrated.

## Deferred/research orientation

- Station radio rendezvous/legal-channel/ALE-style work remains component-local research in `OceanMail/oceanmail-station/docs/research/RADIO_RENDEZVOUS_AND_LINK_REQUIREMENTS.md`.
- Organization-wide deferred product/network ideas are tracked in `docs/research/wishlist.md`.
- HF rendezvous, frequency-selection, routing/relay, ALE-adjacent, and Emergency-access changes must be screened against `docs/research/patent-risk-and-design-around-register.md` before implementation; that register is an engineering/legal-review gate, not an RF authorization or non-infringement opinion.
- Modem, BBS/dial-up, DTN, and adjacent-system prior art is indexed in `docs/research/parallel-work-and-prior-art.md`.
- These research documents do not authorize physical-radio Phase 5 or speculative global multi-hop routing.

## Constraints

- API LAN exposure must not precede accepted auth/authz;
- reusable mailbox/account secrets must not be sent across shared constrained/radio links as a shortcut; relay/gateway reachability must not imply mailbox authority;
- lab receipt trust is not production cryptographic trust;
- preserve exact upstream pins/integration-delta provenance;
- maintain separation between STORE/TRANSPORT and GRID/CONTROL responsibilities;
- do not reintroduce an ordinary sender-selectable Priority class into relay/gateway logic;
- do not apply eager/reluctant durable-mail relay semantics to ordinary OChat forwarding;
- Station admin authority must not imply another user's private mailbox access;
- local SMTP/Postfix capability must not be interpreted as authority for direct arbitrary public Internet SMTP delivery;
- if central Server is unavailable, retain/retry Internet-boundary work without disabling viable native OMail paths;
- do not assume a particular SBC Wi-Fi driver supports simultaneous AP+STA without real qualification;
- durable storage and crash recovery matter more than large local capacity for permanent Internet-connected gateways.

## Accepted personal-traffic boundary (2026-09-22)

Band 1 is public discovery/route/access coordination plus authorized urgent public updates. Band 2 includes ordinary manifests, requests, receipts, custody/repair/stop-flow/tombstones, account reconciliation, and payload, with expedited mail control within its fairness shares. Bands 0/1/3 are public over HF. Client–own Station, direct Client–Server Internet, and gateway–Server connections are always authenticated and encrypted. Personal HF encryption, if adopted, terminates at Station and Server through untrusted relays/gateways; the deployed path has no plaintext capability or fallback. A single deployment choice remains pending feasibility, not a user or per-message option. External SMTP is a separate boundary without a universal encryption guarantee.

[ADR-009](../docs/decisions/ADR-009-personal-traffic-and-encryption.md) governs follow-on work. Component classification, API/transport security, and key management require implementation and validation; no production capability is claimed by this documentation.

## CI retrofit

Station remains the first application measurement/ratchet target. G0/S1/S2 are historical completed phases; S3a tooling and tracking merged on 2026-09-26. [The public port record](../docs/quality/station-s3a-public-port.md) and [central tracker](../docs/specifications/ci-quality-retrofit.md) record scope and acceptance gates. S3a is merged, with no baseline or CI enforcement activation. S3b/S4 and physical-radio work are not authorized by this port.
