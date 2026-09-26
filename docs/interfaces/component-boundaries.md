# Cross-Component Boundaries

Status: CURRENT

## Desktop ↔ Station

- Standard local SMTP/IMAP may carry ordinary mail-client behavior.
- The ordinary SMTP/IMAP boundary is standards-based rather than OceanMail-Desktop-specific: another correctly configured, authenticated standards-based mail client may interoperate for ordinary mailbox submission/retrieval where the Station exposes those services.
- Such interoperability does **not** make a generic mail client a complete OceanMail client. OceanMail-specific state/control uses the Station API/contract, including Available, evidence semantics, budgets/accounting, Station/Grid/link status, constrained-link planning, and Emergency-specific product behavior.
- Available is private account-scoped remote manifest state, not an IMAP folder or already-local content.
- After Desktop durably hands ordinary mail to the accepted Station/mail-submission boundary, persistent queueing, retries, constrained-link execution, and transport/receipt evidence are Station/STORE-TRANSPORT responsibilities. Desktop does not own a separate authoritative OceanMail Outbox queue.
- Desktop native Sent may display/augment transport or delivery state only from securely correlated, authorized account-scoped evidence. Vessel-wide Station history, Postfix disappearance, subject/recipient/timing matches, and fixture/demo rows are not substitutes for per-message account evidence.
- Sender-visible final delivery must follow [`../specifications/delivery-evidence-and-repair.md`](../specifications/delivery-evidence-and-repair.md); Desktop must not equate local queue departure, transport completion, or an intermediate relay handoff with authoritative destination receipt.
- LAN exposure requires accepted authentication/authorization; current Station implementation remains conservative until that work lands.
- Desktop must not infer or invent missing Station evidence/APIs.

### Phase 4J context-only lab integration (merged laboratory implementation)

Station implements
`GET /api/v1/auth/context` and
`GET /api/v1/accounts/{account_id}/auth/context`, consumed by the explicit lab
adapter in Desktop.
The Station authenticates a runtime-provisioned laboratory credential and
enforces explicit permissions before returning server-derived Station/user/role,
independent device-trust state and account grants. The account endpoint requires
that exact account's context-read grant; role or device trust cannot replace it.

This is loopback synthetic-lab integration only. Desktop tokens stay in memory;
no production enrollment, LAN exposure, holder disclosure, protected persistence,
Available catalog/plan, or accounting policy is selected. The Station's existing
vessel-wide evidence routes remain separate unprotected laboratory diagnostics,
not a bypass for real private-account APIs. Keep the global auth/LAN/storage
capability gates false until their broader acceptance criteria are met. Detailed
wire fields and tests belong in the component documents/PRs.

## Station ↔ HERMES/Mercury

- HERMES/Mercury and Taylor UUCP remain authoritative upstream/store-transport components for their responsibilities.
- SMTP and IMAP terminate at the local mail-service boundary; they do not traverse the constrained link. The constrained middle remains HERMES/UUCP/Mercury (or another accepted Station transport), preserving bandwidth-sensitive store/forward behavior independently of the desktop mail engine.
- Station owns OceanMail-specific policy, evidence correlation, state, management, and Grid/control behavior around them.
- Within Station, GRID / CONTROL owns peer/topology observations, relay/gateway policy, OChat Grid behavior, and future selection/routing intelligence; STORE / TRANSPORT coordinates authoritative stores/transports and executes accepted work.
- OceanMail relay/gateway/OChat/routing policy must not be pushed into HERMES, Mercury, Taylor UUCP, Postfix, Dovecot, or a later store/transport adapter merely because it holds or moves the bytes.
- GRID / CONTROL may authorize/select work; STORE / TRANSPORT reports measurable execution/evidence back. This policy/execution boundary is organization-level architecture; see ADR-004.
- Stable logical OMail identity, returned destination evidence, patient query-before-retry behavior, and bounded repair are OceanMail semantics above lower-layer job/session identities; transport success alone cannot manufacture delivery.
- Do not duplicate authoritative payload queues merely to create an OceanMail abstraction.

## Station/Client ↔ Server

- Server owns hosted account/mailbox/service behavior and authoritative global service/accounting state.
- A disconnected Station may hold provisional/local state but cannot invent globally authoritative credit/accounting.
- Station-less hosted/Lite operation must preserve equivalent client authentication, account-grant, durable-plan, and privacy semantics at the hosted service.
- Server may answer delivery/repair queries only for state it actually owns or can authoritatively evidence; Server acceptance, destination mailbox receipt, external-service evidence, and human reading remain distinct claims.
- Internet-connected gateway Stations exchange eligible OMail traffic with Server through an authenticated OceanMail service contract; public Internet SMTP delivery is not a Station responsibility.
- If Server is unreachable, Internet-boundary work may queue/retry locally or in the appropriate authoritative store, while viable native OMail paths continue independently.

## OceanMail Server ↔ external Internet mail/services

- OceanMail-operated Server/infrastructure is the sole public SMTP/MX boundary for OceanMail.
- External services remain independent systems and do not need to understand OceanMail constrained-link transport.
- Gateway Stations are OceanMail transport/gateway participants, not independent public Internet MTAs; they must not deliver directly to arbitrary Internet SMTP systems merely because they have Internet connectivity or local Postfix capability.
- Server/infrastructure owns public-mail concerns including SMTP/MX, destination delivery/retry, bounce handling, DKIM/SPF/DMARC alignment, reputation, abuse/rate controls, and related operational monitoring.
- Exact provider, host count, geography, IP allocation, and scale-out topology are deployment details within this boundary.
- Report only the delivery evidence actually provided by the external service.
- Winlink/SailMail interoperability requires separate technical/legal/service authorization; it is not native OMail by relabeling.

## Native OMail independence

- Native boat-to-boat/store-carry-forward OMail does not require central Server or Internet availability.
- Central Server is required when crossing between native OMail and conventional public Internet mail/services, or when a separately defined centrally managed service requires it.
- A central Internet-mail outage delays the Internet boundary; it must not be interpreted as a network-wide OMail outage.

## Shared change rule

Any change that alters identity semantics, privacy/authorization, delivery-state meaning, gateway/relay policy, accounting ownership, public Internet-mail authority, or cross-component API contracts must be reconciled in this project repository and in each affected component's local implementation documentation.
