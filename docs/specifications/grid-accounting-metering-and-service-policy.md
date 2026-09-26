# Grid Accounting, Station Metering, and Service Policy

Status: CURRENT

This specification defines the durable cross-component accounting and metering relationships for constrained/Grid operation. It deliberately does **not** freeze quota sizes, prices, credit formulas, abuse thresholds, or other operational tuning values.

Current mail scheduling authority also applies: user-originated OMail transport classes are **Emergency** and **Ordinary** only. `Important` is message metadata and must not change RF/Station/relay precedence, gateway/path selection, quota treatment, credit treatment, or automatic Available ordering.

## Capacity units and lease policy

[ADR-008](../decisions/ADR-008-four-band-scheduling-and-channel-use.md) defines Bands 0–3. User/ship budgets use bytes; Station budgets use airtime, with local-account, relay, and system domains kept distinct. These are capacity controls, not new pricing or paid priority.

Lease duration and the normal Band 1 cap are independently configured; ten/four minutes are arithmetic examples, not defaults or a fixed 40% ratio. Necessary route establishment may use the whole lease; otherwise Band 1 is limited by its configured cap. Band 2 uses the remainder with account/relay-peer fairness. Band 3 receives no reserved lease allocation and uses idle or announced shared broadcasts. Authenticated Server promotion moves urgent shared updates to Band 1 under its normal cap. Band 0 overrides ordinary budgets under existing authorization gates.

Account manifests and payload, setup, ACKs, and retries consume attributable Station time; relay does not debit a local account's payload-byte allowance merely for forwarding. Internet-only work consumes no HF airtime. Unused opportunities are released. Lease/cap values and fairness weights remain tunable.

## Mail-specific control placement (2026-09-22)

[ADR-009](../decisions/ADR-009-personal-traffic-and-encryption.md) places ordinary manifests, retrieval requests, message synchronization/resume state, receipts, custody evidence, repair/status, stop-flow/tombstones, and mailbox/usage reconciliation in Band 2 with the associated mail service. Account-specific metadata consumes its account airtime share; relay-specific metadata consumes its relay share. This does not automatically debit user payload-byte quotas. Expedite compact evidence that suppresses unnecessary work and reconsider it between bounded payload batches. Band 1 is public shared network coordination; Emergency control remains Band 0.

## Ordinary constrained-link retrieval requires recipient approval

Ordinary OMail payload content is not automatically retrieved over a metered/Grid/constrained link merely because the message is small.

A recipient may first learn private, account-authorized `Available` metadata describing remote content. That metadata is not authorization to transfer the payload. The recipient selects/approves the ordinary OMail content they want retrieved; the Station may then persist that intent and execute it later when a suitable opportunity exists, including after the client disconnects.

Message size may affect estimates, ordering, representations, and user choice, but does not create an automatic-download exception. Emergency OMail follows its separately accepted Emergency policy.

Ordinary Internet-only synchronization may remain outside constrained/Grid accounting according to current service policy; inexpensive Internet availability does not change the distinction between remote Available metadata and already-local content.

## End-user accounting relationship

For ordinary OMail carried over a metered/Grid/constrained path:

- the **sender pays the applicable send quota** for sending the message;
- the **receiver pays the applicable receive quota** for ordinary content they selected/approved and successfully receive;
- send and receive accounting remain distinct;
- incomplete or unusable receive attempts are not treated as successful receipt for user accounting; and
- Emergency OMail follows its separately accepted quota/exception policy.

The exact accounting event mapping to lower-layer evidence is an implementation contract to be specified consistently with OceanMail's truthful delivery/evidence model. This specification fixes who owns the end-user side of the accounting relationship, not a transport-specific byte counter.

## Relay and gateway traffic is not user-billable forwarding

A Station carrying third-party relay/gateway traffic does **not** debit the vessel's, captain's, or another local user's ordinary send/receive Grid quota merely because that Station handled the traffic.

From the end-user quota perspective, third-party relay/gateway work therefore behaves as though it has an unlimited user-quota budget.

That phrase means only **no end-user quota debit**. It does not mean unmetered, unlogged, physically unlimited, or exempt from local resource policy.

## Meter everything useful to operations; charge selectively

The Station needs a budget/resource-accounting architecture broader than customer quota enforcement. It should maintain distinct evidence domains for at least:

1. **End-user Grid accounting** — local users' constrained send/receive usage and eligibility.
2. **Relay/gateway resource accounting** — third-party work carried by the Station.
3. **Station/system operational accounting** — control, manifest, receipt, policy, synchronization, retry, diagnostic, and other Station work.
4. **Contribution evidence** — evidence needed to evaluate eligible relay/gateway contribution without allowing the Station to mint credit itself.

Where the selected transports expose reliable measurements, useful evidence includes:

- application/user payload bytes;
- Station/protocol overhead;
- third-party bytes received, held, forwarded, or gatewayed;
- RF airtime or on-air-equivalent duration;
- Internet/gateway bytes, especially on metered links;
- relay storage and duration held;
- retries, duplicate traffic, repair/retransmission, and control chatter;
- peer/source traffic rates and repeated failure patterns;
- power/CPU/storage pressure where operationally useful; and
- success/failure/receipt outcomes and timestamps.

Do not invent measurement precision that the underlying transport does not expose.

## Relay resource controls and abuse handling

Because third-party work is metered separately from user billing, the Station may enforce operator/service resource policy without converting relay traffic into a local user's billable mail activity.

Possible controls include RF-airtime ceilings, third-party byte limits, relay-storage ceilings, retry/control-chatter limits, source/peer rate limits, battery/power thresholds, CPU/storage-pressure limits, metered/satellite Internet permissions, quiet/operational windows, and local-work/Emergency preemption.

A Station may locally rate-limit, defer, deprioritize, or temporarily refuse excessive, defective, inefficient, or abusive third-party work according to current policy while preserving accepted Emergency behavior and required local/system work.

## Station management of end-user budgets while disconnected

A Station may manage constrained-link budget eligibility on behalf of its authenticated users while clients are offline.

The Station should be able to:

- cache current applicable service policy and account allowance state;
- maintain durable local working ledgers;
- expose authorized budget/eligibility state to clients;
- persist user approval for a specific queued send or retrieval operation;
- prevent work that is not currently authorized by the applicable budget/policy;
- continue previously authorized work after the client closes;
- record actual successful usage/evidence; and
- reconcile later with Server-authoritative account state and policy.

A disconnected Station cannot mint globally authoritative balances or credit. Server reconciliation may confirm, adjust, refund, or otherwise correct provisional local accounting according to current policy.

## Eager-relay contribution credit

Verified eligible **Eager** relay/gateway contribution may earn service credit. Merely enabling Eager mode is not itself sufficient proof of useful contribution.

The Station records candidate contribution evidence. The Server remains authoritative for validation, deduplication, anti-gaming decisions, balances, corrections, and any globally spendable credit.

When a Station is registered, the owner selects the destination for earned Station contribution credit:

- the associated **vessel account**; or
- the **captain's personal OceanMail account**.

The destination is an authenticated Station registration/accounting setting. It is not inferred from which crew member happens to be logged in when relay work occurs. Changing the destination must follow the accepted authenticated settings/account workflow and reconcile with the Server.

## Architecture versus mutable service policy

The relationships above are architecture/product semantics. The following are deliberately mutable service policy/tuning and are expected to change as testing, field capacity, economics, and abuse evidence improve:

- send/receive allowance amounts;
- service-tier quota and pricing values;
- eager-relay qualification formulas and credit rates;
- credit caps, expiry, rollover, and spend ceilings;
- reconciliation/refund thresholds and adjustment rules;
- anti-gaming and abuse-detection thresholds;
- relay/gateway RF-airtime, byte, storage, retry, chatter, peer-rate, power, and metered-Internet ceilings;
- retention durations; and
- similar numeric/economic/operational values.

Changing one of those values does not by itself require a new architecture decision, protocol generation, or client/Station release when the existing authenticated/versioned policy schema can express it. A conceptual change—such as changing who pays, making ordinary payload retrieval automatic, charging volunteer relays user quota, or ceasing to meter relay work—does require architectural reconciliation.

These tuning values should not be recorded as unresolved architecture merely because an initial number is not known yet.

## Ownership

- **Project spine:** owns these cross-component accounting/metering semantics.
- **Station:** measures relevant work, enforces cached local eligibility/resource controls, persists working ledgers and user intent, and produces contribution/abuse evidence.
- **Server:** owns authoritative global account balances, service-policy values, reconciliation, credit qualification, billing/service-tier behavior, and cross-Station abuse/accounting decisions.
- **Desktop/future clients:** display authorized budget/estimate state and collect user selection/approval; they do not invent accounting truth when Station/Server evidence is absent.
- **Infrastructure/operations:** deploy and observe Server-controlled policy changes without redefining the accounting relationships.
- **HERMES/Mercury/other transports:** expose lower-layer metrics where available; OceanMail does not recreate or fabricate transport internals for accounting convenience.

## Supersession and rejected interpretations

The following earlier interpretations are not current:

- **Small ordinary OMail auto-download over constrained links:** rejected. Recipient selection/approval is required for ordinary payload retrieval regardless of size.
- **Ordinary sender-selectable Priority affecting quota/credits or transport precedence:** superseded by the Emergency/Ordinary decision. `Important` remains metadata only.
- **Relay Off / old combined gateway-willingness mode lists:** superseded by current Eager/Reluctant relay semantics and separate Full/Minimal/Off gateway policy.
- **`Relay traffic is free` meaning unmeasured/unbounded:** rejected. It means no local end-user Grid-quota debit; the work remains metered and resource-controlled.

Detailed Available privacy/authorization remains governed by the current Station Available/account contract and project identity/privacy rules.
