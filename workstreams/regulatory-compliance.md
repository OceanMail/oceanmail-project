# FCC / U.S. Regulatory Compliance Workstream

## Purpose

Resolve U.S. regulatory questions that materially affect OceanMail radio operation before physical-radio deployment or claims of legal readiness.

## Current status

Physical-radio Phase 5 remains deferred pending explicit authorization and hardware/test scope. The project does not yet have an authoritative FCC determination for the exact operating model contemplated by OceanMail.

The remaining work is narrower than general legal research: obtain sufficiently authoritative guidance for the actual proposed equipment, software/modem behavior, service model, operator/licensing model, frequencies/emission characteristics, automation, test/deployment scenario, and confidentiality/encoding behavior.

The rule findings below are project constraints and issue-spotting, not legal advice or an FCC authorization. They were rechecked against current Part 80/Part 5 material during conversation reconciliation on 2026-09-11.

## Verified U.S. rule touchpoints

### Ship-station authorization

47 CFR § 80.13 does not provide a general license-by-rule path for maritime HF data on a voluntary recreational vessel. Its license-by-rule exception covers specified marine VHF, AIS, EPIRB, and radar operation; other transmissions require a ship-station license.

**Project consequence:** do not design production U.S. maritime HF around an assumption that OceanMail users can transmit under a generic license-free HF regime.

### Operator credential and user control

47 CFR § 80.165 lists **MP (Marine Radio Operator Permit)** as the minimum operator credential for a voluntary ship station using direct-printing telegraphy. It separately lists RP for specified lower-power below-30-MHz ship radiotelephony.

47 CFR § 80.156 permits a qualified operator, when authorized by the station licensee or master, to permit an unlicensed person to modulate the transmitter for modes other than Morse radiotelegraphy.

**Unresolved:** Mercury/OceanMail has not been authoritatively classified as direct-printing/radioprinter, J2D data, radiotelephony, or another Part 80 category. Therefore OceanMail must not yet present MP, RP, or no individual credential as the settled user requirement. If direct-printing classification is confirmed, MP is the rule text currently implicated. The exact mapping from a licensed operator's responsibility to OceanMail accounts/crew actions also requires authoritative interpretation.

### Radioprinter and direct intership operation

47 CFR § 80.1155 provides a voluntary radioprinter framework for ships under 1,600 gross tons. It permits ship-to-associated-private-coast-station radioprinter communication and intership radioprinter operation between ships authorized to communicate with a common private coast station. Traffic is limited to communications associated with the business and operational needs of the ship.

**Project consequence:** Part 80 contains an existing concept relevant to direct vessel-to-vessel digital communication. It does **not** by itself authorize OceanMail's protocol, emission, traffic scope, store-carry-forward relay, multi-hop behavior, or automation.

### HF radioprinter frequencies and bandwidth

47 CFR § 80.373(d) identifies HF radioprinter bands for ship/private-coast communication and states that radioprinter communications in those bands must not exceed 300 Hz bandwidth.

47 CFR § 80.205 separately contains authorized-bandwidth table entries including 280HJ2B/300 Hz, 2K80J2B/3.0 kHz, and 2K80J2D/3.0 kHz. Those generic table entries do not override service/frequency-specific restrictions.

SailMail's published private-coast license WPTG385 is a concrete precedent showing specific 2K80J2B authorizations on assigned frequencies. The mechanism and conditions that reconcile those grants with the ordinary § 80.373(d) radioprinter bandwidth language have not yet been established for OceanMail.

**Unresolved:** determine whether OceanMail/Mercury would require a specific frequency/emission grant, waiver, different service classification, or another authorization path. Another licensee's authorization is precedent to investigate, not permission OceanMail can inherit.

### Automatic and unattended transmission

47 CFR § 80.179 enumerates unattended transmitter operations, including specific NB-DP, selective-calling, AMTS/public-coast, EPIRB, and limited VHF safety cases. It does not provide an obvious general authorization for arbitrary unattended private HF OceanMail store-and-forward transmission.

**Project consequence:** Station must not assume that an automatically queued job may autonomously key an HF transmitter merely because the software can do so. Automatic receive, local scheduling, storage, route selection, operator-authorized transmission, and fully unattended transmitter initiation must remain technically separable until the lawful model is settled.

This is an independent gate on future relay/store-carry-forward research. Current architecture already evidence-gates speculative multi-hop behavior; regulatory permission is an additional requirement.

### Private-coast eligibility

47 CFR § 80.501 includes several private-coast eligibility categories, including a person servicing or supplying noncommercial vessels, an organized yacht club with moorage facilities, and a nonprofit organization providing noncommercial communications to vessels other than commercial transport vessels.

SailMail uses the nonprofit-association/private-coast model. A possible separation between a nonprofit radio-network operator and a commercial OceanMail software/server entity was explored in chat, but **no organizational structure has been accepted**. Eligibility, control, compensation, service scope, and affiliation questions require specialist review before any such structure is adopted.

### Experimental development

Part 5 Experimental Radio Service supports radio research and product-development experimentation under an appropriate authorization. FCC material distinguishes conventional experimental licenses and temporary experimental STAs; the correct mechanism depends on equipment, frequencies, locations, power, emissions, duration, and purpose.

**Project consequence:** Part 5 is a plausible route for controlled over-the-air development not already covered by another lawful authorization, but OceanMail must not assume a generic Part 5/STA filing automatically clears a proposed test. Define the exact test fact pattern first.

## Confidentiality and authentication remain separate questions

For U.S. amateur-radio operation, treat the Part 97 restriction on messages encoded for the purpose of obscuring their meaning as a material constraint unless authoritative guidance establishes a specific permitted exception for the contemplated operation. Do not generalize that rule to all maritime/commercial HF services, and do not assume that one radio-service conclusion applies to every OceanMail transport.

Authentication and confidentiality are separate project concerns. A transport may need strong non-replayable authorization even where message contents must remain monitorable. See `docs/specifications/constrained-link-authentication-privacy.md`.

The maritime-service confidentiality/encryption rules for OceanMail's eventual Part 80 operating model remain unresolved and must be evaluated for the exact service, frequencies, traffic, and jurisdiction selected.

## FCC staff response received 2026-09-04

Kathleen Grace Curameng, Attorney Advisor, Mobility Division, Wireless Telecommunications Bureau, replied to OceanMail's detailed Part 80 inquiry.

The response did **not** answer the substantive questions about emission classification, operator credential, intership store-forward, unattended operation, or private-coast structure. It recommended consulting legal counsel and provided general guidance that RF products must use the applicable FCC equipment-authorization procedure (SDoC or Certification as applicable), frequency use must comply with the Table of Frequency Allocations in 47 CFR § 2.106, and temporary/experimental operation may involve STA/Part 5 procedures.

Treat this response as useful procedural direction but **not** as approval, rejection, or an FCC legal interpretation of the proposed OceanMail HF service.

## SailMail precedent and follow-up

SailMail is the closest established U.S. operating precedent identified so far:

- SailMail describes itself as a nonprofit association of yacht owners operating FCC-licensed two-way private coast stations in the Maritime Mobile Radio Service.
- It describes its service as radioprinter/Internet-email communication for members' private business and operational needs.
- Membership is limited to noncommercial vessels under 1,600 tons.
- Its public terms require member vessels to hold valid ship-station licenses from the vessel's flag administration and to carry copies of SailMail's U.S. FCC coast-station licenses.
- Published SailMail FCC licenses include 2K80J2B authorizations.

Do **not** infer that SailMail implements OceanMail-style mesh/multi-hop relay or that every SailMail operating practice is automatically available to OceanMail. SailMail's normal public architecture is vessel-to-coast email service; § 80.1155's intership provision is a separate regulatory capability to investigate.

A SailMail inquiry was drafted in the retired conversation but there is no Git evidence that it was sent. Follow-up questions remain:

1. What operator credential does SailMail understand to be required on U.S.-flag voluntary vessels using its PACTOR/radioprinter service?
2. How were its 2K80J2B private-coast authorizations obtained, and how does SailMail understand them relative to § 80.373(d)'s 300 Hz language?
3. Which portions of coast-station operation are automatic/unattended in practice and under what authorization?
4. Has SailMail used or formally evaluated § 80.1155 intership radioprinter operation?
5. Has it evaluated vessel-to-vessel store-and-forward relaying?
6. How does it understand the equipment-authorization boundary between an external digital modem and a certified Part 80 marine transceiver?

Public contact identified during research: `support@sailmail.com`.

## Mercury / HERMES regulatory state and follow-up

Mercury remains the preferred open HF modem baseline under ADR-002. Rhizomatica describes Mercury v2 as an open-source HF OFDM modem supporting peer-to-peer ARQ, broadcast data, adaptive modes, and store-and-forward email/file-transfer use cases. Current Mercury documentation exposes configurable `BW500`, `BW2300`, and `BW2750` channel-width selections.

Rhizomatica's public Mercury release states that Mercury is compliant for **amateur use**. No corresponding U.S. Part 80 maritime authorization or classification has been identified. Amateur compliance must not be represented as Part 80 approval.

A Rhizomatica/Mercury inquiry was drafted in the retired conversation but there is no Git evidence that it was sent. Technical questions remain:

1. Has Mercury/HERMES been evaluated under U.S. Part 80 or comparable maritime-mobile rules elsewhere?
2. What ITU/FCC emission designator best describes each current Mercury mode when sent through an SSB transmitter?
3. What are the measured necessary/occupied bandwidth and spectral characteristics for current control and payload modes?
4. Which modes fit 500 Hz, 2.3 kHz, and 2.75 kHz configured operation, and what spectral-mask assumptions apply?
5. Has Mercury been tested with Part 80 marine radios such as the Icom M802/M803 family?
6. What licensing/authorization model has been used for HERMES stations that automatically key HF transmitters?
7. Which current upstream technical documents should be supplied to regulators for waveform, ARQ, PTT/control, bandwidth, and unattended-operation review?

Rafael Diniz was identified in Rhizomatica material as the HERMES/Mercury technical lead and is the preferred first technical contact. Preserve any correspondence outcome in Git rather than relying on email/chat memory.

## Candidate reference radio: Icom IC-M803

The IC-M803 is a strong **candidate**, not an accepted mandatory OceanMail radio. Icom markets it for HF email operation and external modem/NBDP use, and FCC equipment records identify the M803 under FCC ID `AFJ410000` as an MF/HF marine transceiver.

Before treating any specific emission as covered, obtain and archive the relevant official equipment grant/exhibits and verify the exact authorized frequency, power, emission, and conditions. A certified radio does not by itself answer whether OceanMail's waveform, traffic, service, frequency, automation, and operating model are authorized.

## Current project guardrails

Until authoritative resolution:

- do not describe license-free HF, CB, Part 15, or amateur-radio authorization as the production regulatory basis for OceanMail maritime HF;
- do not claim Mercury itself is Part 80 approved;
- do not claim a Part 80-certified transceiver automatically makes every external modem/waveform/use lawful;
- do not claim MP or RP is definitively the OceanMail operator credential until emission/service classification is resolved;
- do not enable or depend on unattended HF transmission merely because Station can automate it;
- do not infer multi-hop/store-carry-forward legal authority from § 80.1155's direct intership language;
- do not infer a commercial/nonprofit organizational structure from SailMail without specialist review;
- do not generalize amateur-radio confidentiality restrictions to other services or vice versa;
- keep physical-radio Phase 5 behind the authorization gate recorded in `CURRENT_STATE.md` and `workstreams/station.md`.

## Questions that still require authoritative resolution

At minimum, determine:

1. the correct Part 80 service/classification/emission designator for the selected Mercury configuration;
2. permissible necessary/occupied bandwidth and frequency assignments for that classification;
3. ship-station and coast-station licensing requirements;
4. operator credential/control requirements for ordinary OceanMail crew/users;
5. the lawful scope of direct intership OceanMail traffic;
6. whether store-and-forward relay is permitted and under what conditions;
7. which automatic or unattended transmitter behaviors are allowed;
8. equipment-authorization implications of the selected radio/computer/modem arrangement;
9. the eligible organizational/service structure for recreational-vessel operation;
10. whether and under what exact service/frequency/jurisdiction payload confidentiality/encryption is permitted, restricted, or prohibited;
11. how authenticated but monitorable/plaintext constrained-link operation should be treated where confidentiality is restricted;
12. the correct Part 5/STA or other authorization path for each proposed field-test stage; and
13. whether a request for clarification, declaratory ruling, waiver, experimental authorization, equipment-authorization inquiry, or another FCC process is the proper vehicle for remaining ambiguities.

Do not infer that a general FCC response, informal discussion, AI analysis, consultant-prepared draft, upstream technical capability, or another licensee's grant constitutes authorization for OceanMail's specific deployment.

## Assistance and outreach strategy

Use outside assistance proportionally rather than defaulting immediately to full retained counsel:

1. Keep the technical/regulatory fact pattern and question list current as the design becomes concrete.
2. Obtain technical answers from Rhizomatica/Mercury maintainers.
3. Obtain operational/regulatory-practice answers from SailMail.
4. Seek pro-bono or supervised assistance from communications/technology law clinics when available.
5. Consider an FCC regulatory consultant or filing-preparation service for procedural/document preparation when legal representation is not required.
6. Use specialized communications counsel for interpretation, representation, or filings where the risk, ambiguity, or FCC procedure warrants it; limited-scope review is acceptable.
7. Return to the FCC through the appropriate formal/informal pathway only after the technical configuration and remaining questions are sufficiently specific.

AI may assist with rule research, issue spotting, technical descriptions, draft questions, and draft filings, but must not be treated as legal authority or the source of final regulatory clearance.

## Evidence required before clearing the physical-radio gate

Record in Git:

- the exact factual configuration evaluated;
- selected radio and its official FCC equipment-authorization evidence where applicable;
- selected Mercury/HERMES version/modes and measured bandwidth/emission evidence;
- the relevant FCC rule sections/orders or other primary authority;
- ship/coast/operator license assumptions actually relied upon;
- the confidentiality/encoding assumptions actually relied upon;
- the filing/inquiry mechanism used, if any;
- the authoritative response, authorization, license, grant, or counsel conclusion relied upon;
- scope and conditions of that conclusion; and
- any resulting product, Station, Infrastructure, Server/gateway, hardware, operating, confidentiality, or test restrictions.

If the answer is conditional or ambiguous, preserve that ambiguity instead of marking the workstream complete.

## Ownership and boundaries

This is organization-level regulatory work because its conclusions may constrain Station, Infrastructure, Server/gateway operation, supported transports, hardware, and field testing. Component-specific implementation changes belong in the owning repository after the regulatory constraint is settled.

The human owner remains final authority for regulatory and safety-sensitive decisions under `AGENTS.md`.

## Immediate next action

Obtain the missing SailMail and Rhizomatica/Mercury operational/technical facts, then use the resulting concrete configuration to determine the correct FCC/counsel pathway for authoritative answers, including confidentiality/encoding assumptions.

## Primary references retained for follow-up

- 47 CFR § 80.13 — station license required: https://www.ecfr.gov/current/title-47/section-80.13
- 47 CFR § 80.156 — control by operator: https://www.ecfr.gov/current/title-47/section-80.156
- 47 CFR § 80.165 — operator requirements for voluntary stations: https://www.ecfr.gov/current/title-47/section-80.165
- 47 CFR § 80.179 — unattended operation: https://www.ecfr.gov/current/title-47/section-80.179
- 47 CFR § 80.205 — bandwidths: https://www.ecfr.gov/current/title-47/section-80.205
- 47 CFR § 80.373 — private communications frequencies: https://www.ecfr.gov/current/title-47/section-80.373
- 47 CFR § 80.501 — supplemental private-coast eligibility: https://www.ecfr.gov/current/title-47/section-80.501
- 47 CFR § 80.1155 — radioprinter: https://www.ecfr.gov/current/title-47/section-80.1155
- FCC Part 5 Experimental Radio Service: https://www.ecfr.gov/current/title-47/chapter-I/subchapter-A/part-5
- SailMail terms: https://sailmail.com/cost-and-application-process/terms-and-conditions/
- SailMail example FCC license WPTG385: https://sailmail.com/wp-content/uploads/2021/10/wptg385.pdf
- Rhizomatica Mercury release: https://www.rhizomatica.org/rhizomatica-releases-mercury-a-fully-open-source-modem-for-data-communications-on-hf/
- Mercury upstream repository: https://github.com/Rhizomatica/mercury
