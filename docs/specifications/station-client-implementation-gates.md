# Station/client implementation gates

Status: current blocker/implementation handoff, 2026-09-21. This records existing
accepted constraints and open decisions; it does not approve a production model.

## Merged laboratory work and remaining reviews

Station #47 merged after current-base Phase 4I run `35559385475` passed,
in addition to the prior repeated no-radio readiness/receipt proof and resolved review.
Station #48 has merged #23's bounded Phase 4J laboratory credential/context
slice; merged Desktop #22 consumes its actual endpoints. Desktop #24's bounded
CI also merged.

Desktop #23 remains open for actual Thunderbird Hold/Resume and attachment-only
ordering acceptance. Its refreshed-head run `35559386545` passed and its review
finding is resolved. Owner authorization to merge ready work was given on
2026-09-21; required live acceptance remains separate.

The merged slices are laboratory capability, not production approval. Exact
heads and CI are recorded in the component PRs and CURRENT_STATE.md.

## BLOCKED / ARCHITECTURAL DECISION REQUIRED

### Observed

The Available logical contract is accepted, but it deliberately leaves concrete
holder trust, identity/enrollment, background grant lifetime/revocation and
protected persistence unresolved. Phase 4J only proves runtime lab credentials,
explicit local account grants and independent device-trust representation.

### Why current design cannot yet be promoted to real Available

A successful local bearer context does not authenticate the remote holder or
bind its advertised logical message/components to the intended account. Current
SQLite is plaintext; the storage gate prohibits promoting it to a production
private catalog or pending-operation store. A persisted selection cannot safely
be executed after grant expiry/revocation without an accepted lifetime policy.
There is no authoritative account ledger from which to infer spend eligibility.

### Evidence

- [Available logical contract](https://github.com/OceanMail/oceanmail-station/blob/main/docs/AVAILABLE_MANIFEST_ACCOUNT_CONTRACT.md):
  holder-side privacy, exact account/object binding, durable compare-and-update,
  grant rechecks and required revocation/expiry rules before execution.
- [Storage/key-separation gate](https://github.com/OceanMail/oceanmail-station/blob/main/docs/PHASE4_STORAGE_SECURITY.md):
  no production private state/credentials unencrypted at rest; Station Admin
  does not inherently hold another user's content keys; API remains loopback.
- [Identity workstream](../../workstreams/identity-accounts.md) and
  [constrained-link authentication](constrained-link-authentication-privacy.md):
  enrollment/recovery/device proof/disconnected lifetime remain unresolved.
- [Accounting policy](grid-accounting-metering-and-service-policy.md):
  Server-authoritative balances/credits; Station cannot mint credit; unknown is
  neither zero nor unlimited; retrieval approval and successful receipt differ.

### Decisions needed before real-account execution

1. **Identity/grants:** accepted native/hosted enrollment, device-bound proof,
   revocation propagation and disconnected grant lifetime. Define when a Station
   may continue already-approved work without a connected client or Server.
2. **Holder/object trust:** source-bound logical message/component/representation
   identity and recipient-authorized metadata disclosure. A source fixture or
   RFC Message-ID alone must never stand in for this boundary.
3. **Persistence/unlock:** protected metadata/intent/credential storage and the
   key availability needed for unattended work without giving Captain/Admin
   personal-content access. API auth alone does not settle encryption.
4. **Execution/accounting:** reservation/release and safe in-flight treatment on
   hold/revoke/expiry, including known policy freshness. Keep unknown allowance
   unavailable and new spending blocked; do not block protective hold/defer.

### Options

- Continue pure/synthetic lab validation behind explicit laboratory labels while
  keeping all production gates false. This is useful testing, not real manifests
  or a promise of completion of #24.
- Select and record the narrow production identity/trust/storage/lifetime slice,
  then implement real holder ingestion, private durable plans and accounting
  consumption under those accepted rules.

### Recommended next step

The bounded Phase 4J context and Desktop consumer have merged. Resolve a
single coherent identity/trust/storage/lifetime slice before enabling real
Available. Retain recipient intent as non-executable when authorization/policy
is unknown; do not infer continued execution or arbitrary emergency exemptions.
The exact in-flight behavior still requires an explicit decision. No speculative
crypto, plaintext-production credential store or invented balance should be used
to bypass this gate.

### Affected repositories/files

- Station: `src/auth.rs`, future Available/plan/accounting handlers/storage,
  `docs/AVAILABLE_MANIFEST_ACCOUNT_CONTRACT.md`, `docs/PHASE4_STORAGE_SECURITY.md`.
- Desktop: `extension/station/`, Available source/intent adapter and contract gaps.
- Server: hosted account/grant/ledger authority and Station-less equivalents.
- Project: identity workstream, constrained-link privacy, accounting and this
  decision record. Physical-radio Phase 5 remains excluded.

## Merge boundary

All remaining open PRs remain subject to independent review, exact-head evidence and
explicit owner merge authorization. Readiness is not merge permission. Use merge
commits, then retire branches only after confirming no unique work remains.
