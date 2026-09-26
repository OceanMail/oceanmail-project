# Desktop Workstream

## Purpose

Deliver the OceanMail desktop client/product experience on a pinned Thunderbird foundation while preserving truthful constrained-link semantics and coexistence with stock Thunderbird.

## Repository

`OceanMail/oceanmail-desktop`

## Current architecture

- dedicated OceanMail application package based on Thunderbird;
- native Thunderbird application shell/Spaces rather than a second primary nav rail;
- ordinary local mail mechanics reuse Thunderbird/SMTP/IMAP;
- OceanMail-specific Available, evidence, Station/Grid status, budgets, Emergency behavior, and controls use OceanMail contracts/APIs;
- Available is account-scoped remote/private manifest state, not IMAP or already-local mail;
- accepted account Mail presentation is `Inbox / Available / Saved / Drafts / Sent / Trash`; there is no user-facing OceanMail Outbox;
- Emergency is the only user-originated transport-precedence class; Important is interoperable message metadata only.

## Current implementation state

Desktop PR #7 is the live-verified alpha baseline. Final local verification used Debian/KDE, pinned Thunderbird 140.14.0esr, and the real two-account SMTP/IMAP development lab. It proved cold-start initialization, account-scoped Available/Saved/Sent integration, Local Folders/Outbox hiding in the dedicated profile, restart idempotence, truthful uncorrelated Sent status, native Important metadata, and the accepted Cards/Table alpha compromise. Component evidence lives in `desktop/docs/ui-review/README.md` and `desktop/docs/MAIL_MODEL_CORRECTION.md`.

Desktop PR #13 merged the Available/account/privacy documentation reconciliation against Station PR #26. It records the current logical contract, privacy boundary, fixture limitations, planner defects, and implementation prerequisites; it does not claim that the real Available API is implemented.

Desktop PR #15 merged organization project-spine integration. The former Desktop governance PR #14 was closed as superseded because organization-wide AI/contributor governance belongs in `OceanMail/oceanmail-project`; Desktop retains only component-specific constraints locally.

Desktop PR #21 merged the final chat-preservation design reconciliation for OChat transmission evidence, consent-based location/contact-card flows, Grid geographic/topology visualization, Dashboard/Grid visibility, and gateway-policy presentation. These are accepted design documents, not claims that the corresponding Station APIs or live Grid evidence are implemented.

## Constraints

- do not fork Thunderbird without explicit architecture approval;
- do not create a second primary navigation shell;
- preserve stock Thunderbird coexistence and keep OceanMail profile-specific changes from affecting a separate stock Thunderbird profile/install;
- only explicitly identified/provisioned OceanMail accounts receive OceanMail-specific Mail modifications;
- do not invent missing Station APIs/evidence or use client-side filtering as backend authorization;
- fixture/demo state must remain visibly non-production;
- Sent evidence must remain truthful: no subject/recipient/timing/demo matching and no upgrading Postfix disappearance to delivery;
- Windows/macOS/Linux portability remains a continuous Desktop constraint;
- real Thunderbird lifecycle/chrome behavior requires LIVE / PRODUCT verification when static or CI evidence cannot prove it.

## Accepted alpha-specific behavior

- Thunderbird Cards View cannot render the custom OceanMail Status column and the Cards/Table mode is a global Thunderbird preference, so OceanMail does not globally force Table View; the Sent banner truthfully reports the current mode and provides a view-mode-independent Sent-details path.
- Native Local Folders remains internally available to Thunderbird but is hidden in the dedicated OceanMail profile so Thunderbird's Local Folders Outbox is not exposed as a user-facing OceanMail destination.
- Generic Thunderbird Chat is hidden until real OChat exists. Tasks may remain visible where Thunderbird offers no safe Tasks-only hide mechanism without broader chrome mutation; Address Book-to-Contacts relabeling remains cosmetic/non-blocking unless a clean supported approach is found.

## Major outstanding work

The laboratory client consumes the Station auth-context endpoints without normal
UI provisioning or persisted tokens. Public [PR #1](https://github.com/OceanMail/oceanmail-desktop/pull/1)
adds Dashboard/Watch stale-render guards; [PR #2](https://github.com/OceanMail/oceanmail-desktop/pull/2)
repairs the cross-component auth runner. Neither replaces fixtures with a real
Available service. Live Thunderbird Hold/Resume, attachment ordering and
stale-render acceptance remain outstanding.

- replace Available fixtures with authenticated account-scoped Station capabilities as Station identity/auth/account-grant/API work lands;
- define and implement the real Available manifest/retrieval operations and authoritative accounting behavior without promoting fixture booleans/credits into production contracts;
- add trustworthy per-message Sent evidence correlation as Station exposes it;
- implement real OChat only after the required live Station/transport evidence contract exists; do not turn pending text into a sent transcript entry prematurely;
- continue real Thunderbird integration/live verification for lifecycle/native-chrome changes;
- packaging/install/update identity and production readiness;
- defer mobile until Desktop is mature enough to be the reference experience.

## Accepted personal-traffic boundary (2026-09-22)

Band 1 is public discovery/route/access coordination plus authorized urgent public updates. Band 2 includes ordinary manifests, requests, receipts, custody/repair/stop-flow/tombstones, account reconciliation, and payload, with expedited mail control within its fairness shares. Bands 0/1/3 are public over HF. Client–own Station, direct Client–Server Internet, and gateway–Server connections are always authenticated and encrypted. Personal HF encryption, if adopted, terminates at Station and Server through untrusted relays/gateways; the deployed path has no plaintext capability or fallback. A single deployment choice remains pending feasibility, not a user or per-message option. External SMTP is a separate boundary without a universal encryption guarantee.

[ADR-009](../docs/decisions/ADR-009-personal-traffic-and-encryption.md) governs follow-on work. Component classification, API/transport security, and key management require implementation and validation; no production capability is claimed by this documentation.
