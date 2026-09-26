# Constrained-Link Authentication and Privacy Requirements

Status: current cross-component security requirements; exact production mechanism remains unresolved.

## Purpose

OceanMail may operate over radio and other links where transmissions are observable by unintended receivers, where confidentiality may be unavailable or legally/operationally inappropriate, and where intermediate Stations/gateways may forward traffic without being trusted as mailbox principals.

Authentication, authorization, integrity, and confidentiality are therefore separate concerns and must not be conflated.

## Required security properties

### Reusable mailbox secrets must not traverse shared constrained links

A reusable mailbox password, recovery secret, long-lived bearer token, private key, or equivalent credential MUST NOT be transmitted over a shared radio/constrained link merely because the payload is compressed, encoded, framed, or otherwise non-human-readable.

Reversible encoding and compression are not confidentiality mechanisms.

The eventual production design SHOULD prefer non-replayable proof of authorization (for example challenge/response or device-bound cryptographic proof) over repeatedly sending a reusable account secret. The exact enrollment, credential, and proof mechanism is still an identity/account workstream decision.

### Authentication is independent of confidentiality

OceanMail must be able to authenticate and authorize mailbox/control operations even when message content is intentionally monitorable or unencrypted on a particular transport.

Conversely, encrypting content does not by itself authorize the sender to retrieve, acknowledge, delete, or mutate mailbox state.

### Relay/gateway carriage does not grant mailbox authority

An intermediate Station, relay, gateway, transport peer, or third-party carrier may need enough routing/service information to carry an OceanMail object, but that role MUST NOT automatically receive reusable mailbox credentials or authority to list, retrieve, delete, or modify a user's private mailbox state.

This requirement applies whether the forwarding path is direct, gateway-based, multi-hop, or uses a future external-service bridge.

### Device trust is not account authorization

Consistent with the project security baseline, possession of a trusted device or Station role is not sufficient by itself to access another user's account-private mailbox/Available state. Authorization must resolve to the intended account/user scope.

### Replay and destructive operations require explicit treatment

The production protocol/API must prevent captured/replayed constrained-link traffic from being sufficient to repeat privileged mailbox operations.

Irreversible destructive actions such as permanent message deletion require an explicitly defined, idempotent and recoverable synchronization model. Whether this is implemented through tombstones, retention windows, delayed purge, server-authoritative reconciliation, or another mechanism remains unresolved; a constrained-link `DELETE` command must not be assumed safe merely because the session was once authenticated.

## Confidentiality model

OceanMail must distinguish at least:

- **authentication/authorization** — who may perform an operation;
- **integrity/authenticity** — whether a command/message proof is valid;
- **confidentiality** — whether observers can read content;
- **transport/service legality and policy** — whether confidentiality or particular traffic is permitted on the selected link/service.

A published or open protocol is not inherently non-private: confidentiality can come from cryptographic keys rather than secrecy of the protocol. Equally, an encoded/compressed open-format transmission is not private merely because casual listeners cannot read it without software.

## Accepted connection boundaries (2026-09-22)

| Connection | Accepted policy |
| --- | --- |
| Client ↔ own ship Station | Always application-connection encrypted and authenticated over Wi-Fi, Ethernet, or another local network. Local-network security alone is insufficient. |
| Client ↔ OceanMail Server directly over Internet | Always application-connection encrypted and authenticated, including hosted/Station-less operation. |
| Ship Station ↔ OceanMail Server over an HF/relay/gateway path | If Band 2 encryption is adopted, personal content and metadata remain encrypted through intermediaries. Encryption terminates at the Station and Server, not at a forwarding gateway. |
| Gateway ↔ Server over Internet | Always an authenticated encrypted connection; it can carry the already-encrypted personal objects. |
| Server ↔ external mail provider | A separate SMTP transport-security boundary. Encryption depends on destination support and delivery policy; universal encrypted external delivery is not claimed. |
| External recipient ↔ their provider | Controlled by that provider and the recipient's client. |

The client, own ship Station, OceanMail Server, and relevant external mail provider can process plaintext. Relay Stations and gateways do not receive personal decryption keys merely because they carry traffic. This is not user-to-user E2EE excluding the OceanMail Server or own ship Station.

The Station and Server can prepare/compress content before encryption on their respective outgoing protected paths. Forwarding nodes do not need plaintext for carriage. Packet framing, nonpersonal routing fields, and visible traffic patterns require a minimized outer envelope; detailed field classification remains protocol design work. No claim of anonymity or hidden RF activity is made.

Direct native Station-to-Station delivery remains an existing architectural capability. Its exact encryption/key boundary must be reconciled before implementation; this decision does not silently force all native delivery through the Server or authorize plaintext native exceptions in an encrypted deployment.

## Failure and independent security requirements

If encryption is selected, missing/untrusted keys, unsafe nonce/random state, encryption errors, or incompatible security formats block personal transmission. Corrupt or unauthentic ciphertext is rejected. Recovery is queueing, retry, repair, or an explicit error—not plaintext transmission.

Radio disconnection is a transport failure. Already-sealed objects may be retained and retransmitted/resumed without plaintext exposure. Key recovery, authenticated key distribution, rotation, offline validity, replay protection, and safe storage remain security design requirements.

Authentication, integrity, authorization, and replay protection are required independently of confidentiality. Public messages cannot confer mailbox authority. Reusable passwords, private keys, and long-lived bearer secrets must not be sent over shared plaintext HF links.

Public Emergency traffic retains existing technical, legal, and authentication/authorization gates. Public bands do not imply permission for arbitrary transmitters to issue trusted commands.


## Deployment choice and band confidentiality

[ADR-009](../decisions/ADR-009-personal-traffic-and-encryption.md) makes Bands 0, 1, and 3 public/unencrypted over HF. All ordinary personal content and metadata/control belong in Band 2. Encryption is a single product/deployment decision pending legal, technical, operational and cost feasibility, not a user toggle or per-message negotiation. Prefer Station-to-Server protection through intermediaries if practical and supportable; otherwise deliberately select a plaintext deployment. Neither outcome is yet selected. If encryption is adopted, the deployed personal-traffic path MUST have no plaintext transmission capability, fallback code path, or downgrade setting. Designing for either eventual outcome does not require shipping both modes.

## Radio/legal boundary

Do not assume one encryption rule applies to all HF/radio operation. Permission to obscure/encrypt content depends on the radio service, license, frequency/allocation, jurisdiction, and operational context.

For U.S. amateur-radio use, the project must treat the Part 97 restriction on messages encoded for the purpose of obscuring their meaning as a material design constraint unless authoritative legal/regulatory guidance establishes a specific permitted exception for the contemplated operation.

Maritime/commercial and other radio services have different rule sets. The project currently has no blanket determination that encrypted OceanMail payloads are permitted or prohibited across all contemplated marine HF operation.

Any production route/transport policy that can select among differently regulated links must eventually carry enough policy/capability information to reject a route that is technically available but legally or operationally unsuitable for the message.

## External-network lessons

Historical OceanMail research examined Winlink and SailMail as prior art. The durable lesson is architectural rather than a current integration commitment:

- mailbox/account authentication can be protected independently of radio message confidentiality;
- radio-email systems may deliberately operate with monitorable content while still preventing arbitrary mailbox access;
- external-service rules remain binding when OceanMail carries or bridges traffic for that service.

Current OceanMail 0.2 does not make Winlink or SailMail interoperability part of the critical path. These are research topics, not current interoperability commitments.

## Ownership

- Server owns hosted account/authentication/recovery and server-authoritative mailbox permissions.
- Station owns authenticated local/edge API enforcement and must not fabricate authorization from transport reachability or Station role.
- Desktop/future clients consume these mechanisms and must not embed reusable radio mailbox passwords as a shortcut.
- Infrastructure owns secure credential deployment/storage mechanisms for hosted systems, not account semantics.
- Regulatory work owns authoritative conclusions about which confidentiality modes are permitted on specific radio-service deployments.

## Unresolved design work

The following remain open and must be settled before production security claims:

1. account/user/device enrollment and recovery;
2. device credential/key provisioning and revocation;
3. constrained-link non-replayable proof format and byte cost;
4. offline/disconnected authorization lifetime and reconciliation;
5. destructive mailbox-operation semantics and retention/purge behavior;
6. production cryptographic trust for receipts and private holder disclosure;
7. per-transport confidentiality/legal capability representation;
8. storage encryption and per-user key separation.
