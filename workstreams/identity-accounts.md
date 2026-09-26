# Identity and Accounts Workstream

## Purpose

Define and implement consistent identity, authentication, authorization, device trust, account privacy, and hosted/Station ownership across OceanMail.

## Primary repositories

- `OceanMail/oceanmail-station`
- `OceanMail/oceanmail-server`
- `OceanMail/oceanmail-desktop` as consumer/UI

## Current accepted boundary

- user/account identity, device trust, and Station role are distinct concepts;
- Captain/Admin operational authority does not inherently grant another user's private mailbox/Available access;
- authenticated principal-to-account grants are required before disclosing account-private Available/plan/accounting state;
- Station-less hosted/Lite operation must preserve equivalent authentication/grant/privacy semantics at the Server;
- holder-side private manifest metadata must be recipient/account-authorized or equivalently end-to-end confidential before disclosure;
- native boat-to-boat availability must not depend on central Server availability;
- reusable mailbox passwords, long-lived bearer credentials, private keys, or equivalent reusable secrets must not be sent across shared constrained/radio links merely because a payload is compressed or encoded;
- authentication/authorization and message confidentiality are separate properties: monitorable/plaintext transport does not remove the requirement for strong authorization, and encrypted content does not itself authorize mailbox operations;
- intermediate relay/gateway/transport roles do not inherit mailbox authority or reusable mailbox credentials;
- constrained-link replay resistance and destructive mailbox operations require explicit production semantics rather than assuming a previously authenticated session makes replayed or irreversible commands safe.

Detailed cross-component constraints are in [`../docs/specifications/constrained-link-authentication-privacy.md`](../docs/specifications/constrained-link-authentication-privacy.md).

## Current implementation state

Station issue #23 is the foundational authenticated permission-scoped API/account identity work. Issue #24 is blocked on it. Production storage/key-separation remains independently unresolved.

[Station #48](https://github.com/OceanMail/oceanmail-station-archive/pull/48) and
[Desktop #22](https://github.com/OceanMail/oceanmail-desktop-archive/pull/22) have merged the
bounded Phase 4J lab-context implementation/consumer. Runtime-provisioned tokens
are not production enrollment, device-bound proof, a protected credential store
or disconnected authorization policy. No real multi-user/LAN release is implied.
The exact remaining decisions and safe boundaries are recorded in
[`station-client-implementation-gates.md`](../docs/specifications/station-client-implementation-gates.md).

The historical Server prototype contains MFA/authentication work that may be useful but must be ported deliberately into active 0.2 architecture.

## Outstanding organization-level decisions

- final account/user/device enrollment and recovery model;
- production credential/key storage model;
- device-bound credential provisioning/revocation and constrained-link non-replayable proof format;
- offline/disconnected authorization lifetime and Server/Station reconciliation;
- recoverable/idempotent semantics for destructive mailbox operations and final purge;
- exact cryptographic trust for holder disclosure and receipts;
- reconciliation of disconnected Station state with Server-authoritative global state.
