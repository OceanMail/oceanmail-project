# ADR-009 — Personal-traffic placement and encryption boundaries

Date: 2026-09-22
Status: ACCEPTED DESIGN; implementation and production security validation remain outstanding.
Authority: owner's 2026-09-22 band-placement and encryption-boundary decisions.

## Decision

Band 1 coordinates shared network access and reachability. Band 2 performs ordinary personal mail service, including the metadata and control needed to discover, request, transfer, and reconcile mail. Band 0 retains Emergency payload and its associated control. Band 3 carries ordinary public background updates.

Public HF traffic in Bands 0, 1, and 3 is unencrypted. Personal Band 2 confidentiality is a product/deployment decision that remains pending legal, operational, technical, and cost feasibility. It is not a user choice or a per-connection negotiation between plaintext and encryption.

If encryption is adopted, all personal Band 2 content and metadata must be encrypted from the originating ship Station to the OceanMail Server, and from the Server to the receiving ship Station. Relays and gateways carry ciphertext without access to personal plaintext. The deployed personal-traffic path must have no plaintext transmission capability, fallback mode, downgrade setting, or negotiation outcome.

If encryption is not practical and supportable, the project may instead deliberately select a plaintext Band 2 deployment. Neither outcome is selected by this decision. Designing while this is unresolved does not require shipping both modes.

## Band placement

| Band | Included traffic |
| --- | --- |
| 0 — Emergency | Emergency announcements, coordination, payload, receipts, duplicate suppression, stop-flow, and tombstones. Public over HF. |
| 1 — Shared network coordination | Station discovery/presence, contact requests, relay/gateway availability, reachability advertisements, route establishment and repair, public Grid state, Station-level channel/time negotiation and airtime grants, shared-broadcast announcements, and authenticated Server-promoted urgent public updates. Public over HF. |
| 2 — Ordinary mail service | Personal manifests/Available metadata, retrieval requests, message/component inventories, partial/resume state, custody evidence, destination receipts, repair/status probes, ordinary stop-flow and delivery tombstones, mailbox and usage-accounting reconciliation, bodies, and selected attachments. Both local-account and third-party relay service remain here. |
| 3 — Public background | Ordinary shared datasets, configuration, software, firmware, and other public background updates. Public over HF; eligible urgent updates may be promoted by the Server to Band 1. |

Classification follows purpose: network-level route repair belongs in Band 1; repair of a particular ordinary message delivery belongs in Band 2. Station-level access negotiation belongs in Band 1; account-specific work selection belongs in Band 2. Public control must not expose personal manifests merely to simplify coordination.

Only authenticated, authorized Server designations may promote shared public updates. Important remains message metadata, not sender-controlled transport precedence. Promotion does not make an update Emergency or grant the route-establishment exception.

## Band 2 internal scheduling

The band assignments and confidentiality boundaries are the operating baseline. Detailed in-band ordering and batching remain subject to later refinement; the following records current scheduling intent.

Within a Band 2 opportunity:

1. Process compact delivery evidence, stop-flow, and tombstones that can suppress unnecessary work.
2. Exchange enough authorized manifests, requests, and resume state to select useful transfers.
3. Transfer bounded payload batches.
4. Exchange resulting custody/progress evidence and reconsider pending control between batches.

This is not a requirement to complete every manifest before any payload moves. An account may synchronize Available metadata and finish without requesting content. Ordinary content still requires recipient selection; metadata synchronization does not authorize automatic download.

New stop-flow or delivery evidence must receive expedited processing at the next safe transport boundary rather than wait behind a large attachment or a later lease while redundant data continues to be sent.

Essential link acknowledgments and safe teardown remain part of the exchange they support. Transport-owned framing, ARQ, resume, and authoritative payload stores remain with HERMES/Mercury/UUCP or the accepted transport. This decision does not create a second reliability protocol.

Account-specific metadata consumes the relevant account's airtime share; relay-specific metadata consumes the relevant relay share. This does not automatically debit user payload-byte quotas. Local/relay fairness, account/peer fairness, and truthful Station airtime accounting remain required.

Band 1 retains its normal cap and necessary route-establishment exception; Band 2 uses the available remainder; Band 3 has no reserved share; Band 0 preempts ordinary work. Lease duration and normal Band 1 cap are independent configurable inputs. Ten/four minutes were arithmetic examples, not selected defaults or a fixed ratio.

## Encryption connections and trusted endpoints

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

## Supersession and implementation

This decision supersedes ADR-008's original ordinary-manifest/receipt/control placement and the earlier proposal for runtime plaintext/encrypted selection. ADR-008 and the privacy, delivery-evidence, and accounting specifications are reconciled with this decision. Component traffic classification, private-control formats, key management, and security enforcement remain implementation work; existing laboratory evidence does not prove these requirements. Native direct-delivery encryption remains an explicit unresolved boundary without a plaintext exception. No physical RF authorization or production cryptography is selected here.
