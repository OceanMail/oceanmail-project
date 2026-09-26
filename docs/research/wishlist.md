# OceanMail Wishlist and Deferred Research

Status: **CURRENT parking lot; items here are not implementation commitments unless promoted elsewhere**

## Purpose

Preserve capabilities, experiments, external-project ideas, legal questions, and product improvements that OceanMail would like to explore but which should not delay the current 0.2 critical path.

An item belongs here when it is useful but blocked by scope, maturity, field evidence, legal uncertainty, hardware, cost, upstream ownership, or a conflict with an accepted current boundary.

Current architecture/requirements belong in normal project/component docs. When a wishlist item is promoted, update the authoritative specification/decision and reduce this entry to a link/history note.

Status terms:

- **EARLY PRODUCT** — desirable before broad deployment, but not current proof-path work.
- **RESEARCH** — promising; needs design/measurement before acceptance.
- **WISHLIST** — explicitly deferred.
- **LEGAL REVIEW** — do not freeze product behavior before service/jurisdiction requirements are known.
- **EXTERNAL PROJECT** — could become a separate project rather than OceanMail application work.
- **CONFLICT CHECK** — useful idea that must not duplicate or undermine an accepted upstream/current layer.

---

## Offline user feedback queue

**Status: EARLY PRODUCT**

Provide an in-product way to record feedback while completely offline and submit it automatically on the next suitable ordinary Internet connection.

Candidate structured fields include:

- overall experience rating;
- delivery/link/speed/reliability/ease-of-use ratings;
- issue-category checkboxes/dropdowns;
- operation/transport involved;
- optional free text and feature suggestion;
- optional separately consented diagnostic attachment.

Useful issue categories include connection failure/drop, repeated restart, unexpected slowness, delay/duplication, confusing delivery state, attachment/gateway/relay/radio configuration problems, and UI problems.

Normal feedback should wait for ordinary Internet rather than consume scarce HF/constrained capacity by default. Diagnostics must not silently include mailbox content or other sensitive data.

---

## Progressive constrained synchronization depth

**Status: RESEARCH**

The future compact synchronization/control mechanism should be able to exchange different depths of authorized state according to the quality, expected duration, and cost of an opportunity.

A weak/brief link might exchange only presence/capability, critical receipt state, and minimal object hints. A better opportunity could progressively add logical IDs, sizes, component/representation state, resume information, and other permitted detail.

The goal is to avoid paying the full synchronization cost before learning whether the contact is worth using.

Privacy/account authorization remains mandatory at every depth; progressive synchronization is not permission to broadcast recipient-private Available metadata.

See `../specifications/delivery-evidence-and-repair.md` and Station `AVAILABLE_MANIFEST_ACCOUNT_CONTRACT.md`.

## Adaptive logical transfer inspired by Kermit/ZMODEM

**Status: RESEARCH / CONFLICT CHECK**

Investigate higher-level adaptation such as logical resume granularity, chunk/object boundaries, amount of useful work sent before higher-level reconciliation, and completion-aware scheduling.

Do **not** add a second fine-grained ARQ/retransmission protocol above Mercury, PACTOR, VARA, ARDOP, or another modem/link that already owns that reliability.

Historical inspiration includes Kermit sliding windows/adaptive packet sizing/selective retransmission and ZMODEM streaming/restart. The reusable idea is adaptation to actual link conditions, not copying obsolete framing.

## Batch compression across small objects

**Status: RESEARCH**

Investigate compressing a useful synchronization/transfer batch when that reduces repeated headers and framing.

Any batching scheme must remain interruption-tolerant and should not create one giant compression unit whose loss forces retransmission of all contained work.

## Completion-aware scheduling

**Status: WISHLIST**

Where multiple pieces are eligible, prefer work that completes a useful user-visible object when that provides more value than starting another large incomplete object, while preserving Emergency and current Station scheduling/fairness rules.

---

## Legal/regional channel catalog and rendezvous automation

**Status: RESEARCH; detailed Station-owned work**

Retain the model of deriving usable channel candidates from:

- authoritative legal/service allocations and intended channel purpose;
- operator configuration/licensing;
- radio/modem capability;
- link-quality history/current observations.

Where lawful/supported, investigate rendezvous-set -> negotiate working/data channel -> short link check -> transfer -> return-to-rendezvous behavior, reusing ALE/upstream mechanisms where practical.

Do not invent arbitrary worldwide OceanMail frequencies or repurpose protected distress/safety channels.

Detailed authority: `OceanMail/oceanmail-station/docs/research/RADIO_RENDEZVOUS_AND_LINK_REQUIREMENTS.md`.

## New open software modem

**Status: WISHLIST / EXTERNAL PROJECT**

A clean-sheet OceanMail-specific modem is **not** current 0.2 work.

Only reconsider it if measured field results show that maintained upstream options cannot satisfy required behavior after evaluating Mercury first and, where appropriate, PACTOR, VARA, ARDOP, HERMES Broadcast, FreeDATA/FreeDV/Codec2, and standard radio-control interfaces.

Possible future goals could include open implementation, connected ARQ and broadcast/FEC modes, explicit link-quality APIs, low turnaround overhead, unattended radio control, deterministic simulation, and strong interruption/resume support.

## New network/mesh layer

**Status: WISHLIST / EXTERNAL PROJECT**

Do not build a new global mesh merely because one is imaginable. BEMPIC is frozen and M4P is tabled; the HERMES/Mercury/direct-gateway baseline must be measured first.

A new or revived network layer would require concrete evidence of an unsolved need such as unacceptable routing/scale/overhead, missing store-forward semantics, required cooperative-broadcast behavior, or governance/licensing barriers that cannot be solved upstream.

---

## Trusted local relay / rendezvous service relationship

**Status: RESEARCH**

Investigate explicitly authorizing another Station as a trusted local store-forward/rendezvous node for selected users/vessels without per-message pop-ups.

The relationship should be authenticated and policy-bound. It should synchronize only the state required to perform the service rather than entire historical mailboxes.

A locally useful delivery path should not require unrelated global participation merely because central infrastructure exists.

Current 0.2 still proves direct Station/gateway behavior first; multi-hop execution remains evidence-gated.

## Bounded relay responsibility and path diversity

**Status: RESEARCH; semantics retained, implementation deferred**

Future relay work should evaluate a small bounded number of active responsibility copies (conceptually primary/secondary) plus passive observation/shadow state, rather than global epidemic payload replication.

Relay selection may eventually consider encounter history, reliability, actual destination/gateway reachability, path diversity, geography/ocean basin, movement/heading where appropriate, resource state, and number/freshness of already known copies.

See `../specifications/delivery-evidence-and-repair.md`.

## Contact-opportunity prediction

**Status: WISHLIST**

Use measured encounter history and permitted movement/location evidence to estimate which relay or gateway is unusually likely to help a destination. Treat this as an optimization, never as proof.

PRoPHET-style encounter aging/transitivity is useful prior art.

## Storage-pressure-aware cache diversity

**Status: WISHLIST**

If future relay caches must evict data, prefer retaining scarce/useful/path-diverse objects over data already believed to have strong independent copies, while protecting own-vessel and Emergency requirements according to accepted policy.

## Erasure/fountain-coded large-object dissemination

**Status: WISHLIST**

For large attachments/software/regional data, investigate whether different receivers holding different useful coded pieces materially improves delivery. Evaluate HERMES Broadcast/RaptorQ before inventing a new OceanMail coding system.

Do not add this complexity to ordinary mail without measured benefit.

---

## Direct/one-hop quota model

**Status: RESEARCH / POLICY UNRESOLVED**

Old design work identified a real abuse problem if arbitrary addressed senders can automatically consume a recipient's scarce receive allowance.

Models to compare include:

- sender pays ordinary addressed constrained-link injection;
- recipient pays primarily for recipient-initiated optional/large retrieval;
- relay contribution uses separate voluntary resource policy;
- direct one-hop delivery can receive an efficiency discount because it avoids relay/gateway work, but is not unlimited because it still occupies shared spectrum;
- billing/allowance price remains separate from RF scheduler fairness so cheap traffic cannot monopolize airtime.

No final accounting rule is accepted here. Detailed current research also exists in Station `RADIO_RENDEZVOUS_AND_LINK_REQUIREMENTS.md`.

---

## On-air confidentiality by radio service/jurisdiction

**Status: LEGAL REVIEW**

Do **not** preserve the old blanket statement that all OceanMail email is transmitted unencrypted.

The permitted/required confidentiality model can differ by radio service, jurisdiction, license, commercial provider, and Internet path. Current Available privacy rules also require recipient/account-authorized disclosure of private metadata.

Design future wire/security layers so applicable deployments can satisfy their controlling rules without making end-to-end encryption universally impossible or universally mandatory at the wrong layer.

## Compliance plaintext/export utility

**Status: LEGAL REVIEW / WISHLIST**

Investigate an operator-controlled, documented capability to export legally required records/content in readable form and/or intentionally operate selected storage in plaintext **only when a verified requirement justifies it**.

Do not infer from radio inspection authority that every regulator automatically has a right to all private stored message contents.

This research must not silently create:

- a vendor master key;
- a universal remote decryption backdoor;
- silent regulator/vendor access; or
- weakened default production storage encryption.

Before implementation, map the exact legal process and requirements for relevant FCC radio services, U.S. Coast Guard/compulsory-vessel rules, communications-secrecy obligations, lawful court/subpoena processes, flag-state/port-state requirements, amateur operation if supported, and any public communications-provider obligations.

If OceanMail formally supplies a regulator/authority with a supported export/compliance utility, version the format/tool and maintain an update/contact process for material changes where appropriate.

Production encrypted-at-rest and per-user/private-content separation remain current Station requirements independent of this research.

---

## Historical-tech research queue

**Status: RESEARCH**

Continue mining systems designed around expensive, slow, unreliable, intermittently connected links, including:

- UUCP/rmail/Batch SMTP;
- CSNET PhoneNet/MMDF;
- FidoNet/FrontDoor/BinkleyTerm/Echomail;
- POP2;
- Kermit, XMODEM/SEAlink, ZMODEM and related transfer protocols;
- QWK/Blue Wave offline readers;
- store-forward Usenet;
- CompuServe TAPCIS/NavCIS/B/B+;
- Quantum Link/AOL;
- Prodigy/NAPLPS;
- BPv7/DTN, PRoPHET, Spray-and-Wait;
- contemporary constrained/off-grid systems where they solve the same class of problem.

The maintained catalog is `parallel-work-and-prior-art.md`.

---

# Historical ideas not adopted as current truth

## Topology-dependent user addresses

Do not revive UUCP bang paths or other user addresses that encode the current route. User identity/addressing must survive movement and path changes.

## Delete-on-handoff

A next-hop/relay handoff is not final destination evidence and is not sufficient reason to destroy the source's only repair copy.

## Global blind payload caching / epidemic replication

The earlier idea that every listening Station should record everything it hears was corrected. Passive listening may update useful observations; ordinary payload retention/propagation must be relevant and bounded. Unrelated distant traffic should not fill caches worldwide.

## Fixed universal mail hour

Historic scheduled mail windows are useful prior art, but OceanMail should not require one universal fixed synchronization hour that causes useful opportunistic contacts to be missed.

## Old BBS trust/security assumptions

Borrow efficiency and offline/store-forward ideas, not weak historical authentication or privacy assumptions.

## Modernity as a selection criterion

Do not choose a modern always-online mechanism merely because it is newer. Prefer the mechanism that best satisfies measured constrained-connectivity, security, interoperability, maintenance, legal, and operational requirements.