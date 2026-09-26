# OceanMail Patent-Risk and Design-Around Register

Status: **ACTIVE RESEARCH / ENGINEERING REVIEW GATE**  
Reviewed: **2026-09-22**  
Scope: OceanMail Station HF rendezvous, channel selection, routing/relay, link establishment, and related lower-layer boundaries.

## Purpose

This document records patent families that are sufficiently close to planned OceanMail HF behavior that future implementation should be checked against their claims before the design is changed or physical-radio functionality is released.

This is an engineering screening document, **not a legal freedom-to-operate opinion, non-infringement opinion, or determination that any patent is valid or infringed**. Patent infringement is claim-specific, claim construction can change apparent scope, and the doctrine of equivalents can matter even where literal claim language is not copied. Legal status and territorial coverage must be revalidated from official registers for the jurisdictions in which OceanMail is made, used, sold, offered, imported, or operated.

Google Patents legal-status fields cited below are useful screening data but explicitly state that they are assumptions rather than legal conclusions.

## Current conclusion

No reviewed claim presently establishes that the accepted OceanMail 0.2 architecture requires a patent license.

The current architecture already avoids much of the highest-risk territory because:

- OceanMail is upstream-first for modem, ARQ/FEC, radio-control, and ALE-style link behavior;
- Station owns application/service scheduling, durable state, evidence, authorization, and Grid/control rather than modem DSP;
- a usable next hop is sufficient; OceanMail does not require an end-to-end RF circuit;
- multi-hop routing remains evidence-gated;
- the single-radio baseline uses rendezvous plus pairwise directed exchanges rather than synchronized network-wide relaying;
- no production RF channel-selection algorithm has yet been selected.

The important objective is to preserve those distinctions as the RF design is implemented.

## How to use this register

Before implementing or materially changing any of the following, compare the proposed design against this register:

- rendezvous/calling-channel operation;
- automatic working-channel selection;
- ALE or ALE-like link establishment;
- propagation-aware frequency selection;
- route advertisements or neighbor-state exchange;
- multi-hop relay discovery;
- Emergency propagation/collision avoidance;
- cooperative/broadcast retransmission;
- wideband probing or adaptive link-rate selection.

A design is not considered cleared merely because one literal word differs from a claim. If a proposed design becomes materially close to one of the combinations below, stop implementation and obtain a patent-specific legal review.

## OceanMail design rules

### PR-1 — Keep ALE, waveform adaptation, and RF-link probing below the Station policy layer

OceanMail Station should not implement its own ALE enhancement, wideband training/probing protocol, RF-frame repair, waveform adaptation, or link-rate derivation when an upstream modem/radio can provide the required behavior.

If an upstream product implements patented behavior, delegation alone does not prove OceanMail has a right to use it. Before depending on that behavior for a released product, verify the supplier/upstream project's patent rights, license, authorization, or other applicable right-to-use position.

### PR-2 — Use pairwise next-hop custody, not avalanche/cooperative HF relaying

The preferred OceanMail multi-hop model is:

1. discover or know a candidate next hop;
2. establish a pairwise link;
3. explicitly transfer custody/responsibility for bounded application work;
4. terminate that pairwise opportunity;
5. let the receiving Station independently establish its next pairwise hop.

Do not make the baseline relay mechanism a synchronized network in which two or more relays receive the same RF transmission and then cooperatively retransmit the same or algorithmically related signal in coordinated time slots, subslots, frequencies, or relay windows.

### PR-3 — Do not exchange or merge full connectivity/topology matrices

A Station may retain local observations and multiple local route candidates, but route signaling should remain compact and destination/service oriented.

Preferred advertisement examples include:

- gateway/service identity;
- scalar hop/route metric;
- freshness/age;
- willingness/capability;
- destination-specific reachability;
- locally measured peer success.

Do not implement periodic exchange of complete neighbor/connectivity matrices followed by merging a peer's matrix into the local matrix and computing an end-to-end path from the combined topology.

### PR-4 — Keep rendezvous and working-channel selection simple and distinct from spectrum-harvesting negotiation

A rendezvous channel/set may carry presence, compact contact requests, and an agreed time/channel for a pairwise exchange.

Do not combine all of the following into an OceanMail-owned link-establishment algorithm:

- continuous/periodic spectrum monitoring;
- peer channel-quality probes on a beacon range;
- channel-quality metrics encoded in those probes;
- a beacon link request containing peer location and a proposed out-of-beacon transaction frequency;
- rejection and counter-proposal chosen from the peer's channel-quality metrics;
- a spectrum-occupancy database used to select unused working spectrum;
- false-signal classification based on the absence of an expected probe preamble.

Safer implementation directions are:

- a deterministic/shared schedule drawn from a signed legal channel catalog;
- a small pre-coordinated candidate set with simple pairwise agreement that does not use the claimed probe/occupancy/counterproposal combination; or
- standards-based ALE/link setup performed by a separately reviewed and properly licensed upstream modem/radio.

Do not make vessel/node location a required field of OceanMail's frequency-negotiation proposal.

### PR-5 — Do not make routing a synchronized TDMA/location-neighbor broadcast network

OceanMail must not require all Stations to share synchronized network time, operate a common TDMA BLOS waveform, and periodically broadcast their location plus direct-neighbor information on every frequency in a frequency pick list.

Timing may be used for ordinary scheduling, leases, announced broadcasts, or deterministic rendezvous without turning the entire RF network into this claimed structure.

### PR-6 — Do not implement avalanche call/response link establishment

A calling message or response may be heard by multiple Stations, but OceanMail should suppress redundant responders and select bounded eligible participants.

Do not establish a multi-hop link by having every node in possession of a calling or response message retransmit that message a configurable number of times in coordination with the other nodes that possess it.

Use randomized/backoff/suppression rules to select responders, then establish separate pairwise links.

### PR-7 — Keep propagation data separate from the Skywave fused-stream frequency model

OceanMail may use propagation forecasts or learned link history, but the Station-owned frequency selector should not:

1. collect at least two different data streams that were transmitted to it by skywave propagation;
2. fuse those streams;
3. feed the fused stream into a transmission-frequency model;
4. predict future ionospheric conditions;
5. determine a future optimum working frequency and switch time from that prediction; and
6. transmit at that resulting skywave frequency.

Preferred OceanMail direction:

- use an authoritative signed propagation/channel dataset obtained over ordinary IP or provisioned storage where possible;
- if such a dataset is distributed over HF, treat the signed dataset as one application object rather than separately fusing multiple received skywave telemetry streams in the Station frequency selector;
- use propagation context primarily to select/activate a legal operating profile or prioritize attempts;
- derive the actual working channel by a distinct deterministic rule or delegate selection to a separately reviewed upstream ALE/modem implementation.

### PR-8 — Do not implement the Collins interferer-aware LUF/MUF filtering algorithm

It is acceptable to use ordinary propagation concepts such as legal-band filtering, MUF/LUF information, historical success, or receiver capability separately.

Do not implement the reviewed claim combination that:

- determines LUF and MUF between transmitter and receiver;
- predicts desired received power at the receiver for candidate HF frequencies;
- predicts received power at that receiver from an identified interferer node for the same frequencies;
- removes frequencies outside LUF/MUF;
- determines receiver sensitivity per candidate; and
- removes frequencies where desired received power is both below sensitivity and below the interferer power.

Prefer deterministic profile/channel selection, empirical per-peer success, or upstream link-quality selection without the claimed interferer-power filtering sequence.

### PR-9 — Do not jointly optimize a hypothetical relay position and frequency from modeled link deficit

OceanMail relays are existing participating Stations. They should be discovered/selected from actual available peers.

Do not:

- calculate the maximum link-margin deficit of a direct BLOS path across candidate frequencies;
- convert that deficit into a required range reduction;
- calculate where a relay should be positioned along the source-to-destination direction;
- analyze transmitter-to-relay and relay-to-receiver paths per candidate frequency; and
- use that computation to establish the end-to-end relay path.

Prefer observed reachability, advertised route metric, freshness, policy/willingness, measured link evidence, and store-and-forward opportunity.

### PR-10 — Keep link-quality checks out of patented wideband training sequences

A simple go/no-go link check and use of metrics already exposed by a modem are acceptable design directions.

OceanMail Station should not implement either of these reviewed combinations:

- link request -> confirmation -> known predefined wideband data load -> receiver estimates SNR/BER/channel parameters -> estimates returned -> transmitter data rate selected from those estimates; or
- narrowband ALE link -> wideband/chirp probe -> remote channel-characteristic report -> update the narrowband link based on that probe/report.

These belong, if used at all, inside a separately reviewed upstream radio/modem implementation.

### PR-11 — Keep one working RF channel per pair/session in the baseline

Do not implement receiver-driven dynamic selection of multiple equal-width HF channels followed by simultaneous transmission over the selected set as an OceanMail Station feature.

A modem may internally use multi-carrier modulation as part of its own reviewed waveform; OceanMail should not independently aggregate non-contiguous HF channels to create a parallel application link.

### PR-12 — Keep Emergency collision avoidance above proprietary 4G-ALE mechanics

The future Band 0 Emergency access protocol must not simply reproduce proprietary ALE collision-avoidance mechanisms.

In particular, do not define OceanMail's collision-avoidance PDU as a scan-dwell transmission carrying the specific combination of:

- node identifier;
- call priority;
- maximum call duration;
- transmit-channel identifier; and
- receive-channel identifier

within a 4G-ALE sub-channel-vector scheme.

Similarly, do not adopt network-wide synchronized avalanche relay windows merely because Band 0 needs rapid propagation. Band 0 priority is a Station scheduling rule, not permission to duplicate a proprietary PHY/MAC relay protocol.

## Claim-level register

### HIGH engineering attention

#### US10051606B1 — Efficient spectrum allocation system and method — Rockwell Collins

Screening status: active; Google Patents lists anticipated expiration 2035-09-03.  
Source: https://patents.google.com/patent/US10051606B1/en

Independent claim 1 is close to the generic OceanMail rendezvous -> working-channel concept only after several additional limitations are added: spectrum monitoring, beacon-range channel probes, decoded peer channel-quality metrics, a link request containing peer location and an out-of-beacon transaction frequency, rejection of that proposal, a counter-proposal selected using peer metrics, acknowledgement, and the transaction on the counter-proposed frequency. Other independent claims add spectrum-occupancy profiling and unused-frequency selection.

**OceanMail design-around:** preserve PR-4. Rendezvous plus working-channel negotiation alone is not the design to avoid; the claimed spectrum-harvesting/probe/metric/counterproposal combination is.

**Review trigger:** any proposal to add peer channel-quality sounding, spectrum occupancy maps, or smart counter-proposals to the Band 1 rendezvous protocol.

#### US9282500B1 — Ad hoc high frequency with advanced automatic link establishment — Rockwell Collins

Screening status: active; Google Patents lists adjusted expiration 2034-07-24.  
Source: https://patents.google.com/patent/US9282500B1/en

Independent claim 1 requires a first connectivity matrix of directly reachable nodes, querying a neighbor for its separately generated/stored second connectivity matrix, updating the first with the second, making the first matrix available to the neighbor, and determining a bidirectional path to a third node through those matrices. The claims also include periodic update/query behavior.

**OceanMail design-around:** preserve PR-3. Use compact route/reachability advertisements and local next-hop decisions rather than distributed full-topology matrix exchange.

**Review trigger:** proposals for link-state flooding, full peer neighbor lists, topology databases, or periodic exchange/merge of connectivity tables.

#### US12432794B1 — Avalanche relay linking system — Rockwell Collins

Screening status: active; Google Patents lists expiration 2043-12-27.  
Source: https://patents.google.com/patent/US12432794B1/en

Claim 1 covers call/response link establishment through intermediate nodes where each node possessing the calling or response message retransmits it a configurable number of times in coordination with the other nodes possessing it.

**OceanMail design-around:** preserve PR-2 and PR-6. Discovery can be overheard, but redundant responses are suppressed and selected next-hop links are pairwise.

**Review trigger:** any design where a multi-hop call or response is deliberately flooded/retransmitted by all receiving Stations.

#### US11490452B2 — Ad-hoc HF time frequency diversity — Rockwell Collins

Screening status: active; Google Patents lists expiration 2040-01-21. European family includes EP3855642B1.  
Source: https://patents.google.com/patent/US11490452B2/en

Claim 1 requires two or more relay nodes to directly receive an originating skywave transmission and relay it to a destination in both time-diverse and frequency-diverse fashion using a TDMA waveform.

**OceanMail design-around:** preserve PR-2. Do not use multiple synchronized relay nodes to cooperatively forward the same transmission. Application-layer retries or separately accepted custody copies are distinct design directions.

**Review trigger:** cooperative diversity, simultaneous shadow relays, synchronized duplicate forwarding, or multiple relays intentionally transmitting the same message toward one destination.

#### US11464009B2 — Relays in structured ad hoc networks — Rockwell Collins

Screening status: active; Google Patents lists adjusted expiration 2040-11-28. European family includes EP3876455B1.  
Source: https://patents.google.com/patent/US11464009B2/en

Claim 1 uses TDMA frames divided into slots/subslots; two or more nodes prepare and transmit time-dispersed retransmissions of the first or an algorithmically related signal, dynamically adjust subslot count from network/topology information, and use a negative-acknowledgement subslot.

**OceanMail design-around:** no synchronized subslot avalanche network; pairwise store-and-forward custody only.

**Review trigger:** any attempt to make Emergency or shared broadcasts into coordinated multi-node subslot retransmission.

#### US12375208B2 — Cooperative transmission continuous transmission enhancement — Rockwell Collins

Screening status: active; Google Patents lists adjusted expiration 2043-05-20.  
Source: https://patents.google.com/patent/US12375208B2/en

The independent claims concern multiple-access subslots, an initial transmission that continues past a relay decision point, and coordinated retransmission of the same or algorithmically related signal/message by a relay in a later subslot.

**OceanMail design-around:** same PR-2 boundary; do not build a cooperative PHY/MAC relay system above HERMES/Mercury.

**Review trigger:** coordinated waveform-level relay/retransmission or receiver combining.

#### US12388480B2 — Frequency selection algorithm for resilient HF communication — Rockwell Collins

Screening status: active; Google Patents lists expiration 2044-04-16. European family includes EP4443749B1.  
Source: https://patents.google.com/patent/US12388480B2/en

Claim 1 combines LUF/MUF filtering with modeled desired-signal received power, modeled interferer received power, receiver sensitivity, and a specific candidate-discard rule.

**OceanMail design-around:** preserve PR-8.

**Review trigger:** adding a propagation engine that explicitly calculates desired-versus-interferer received power for each candidate HF frequency and then filters using LUF/MUF and receiver sensitivity.

#### US12501339B2 — Joint optimization of frequency and relay selection for resilient HF communication — Rockwell Collins

Screening status: active; Google Patents lists expiration 2044-03-26. European family includes EP4443976A1.  
Source: https://patents.google.com/patent/US12501339B2/en

Claim 1 determines a direct-path link deficit across candidate HF frequencies, converts it to required range reduction, determines a relay position in the direction between transmitter and receiver, analyzes both relay legs per frequency, and establishes an end-to-end relayed link.

**OceanMail design-around:** preserve PR-9. Select from real discovered Stations; do not calculate where a relay should geometrically exist.

**Review trigger:** joint frequency/relay optimization, link-budget-based relay positioning, or planned relay placement computed from direct-path deficit.

#### US11309954B2 — Technique for selecting the best frequency for transmission based on changing atmospheric conditions — Skywave Networks

Screening status: active.  
Source: https://patents.google.com/patent/US11309954B2/en

Claim 1 collects at least two data streams transmitted by skywave propagation, fuses them, predicts future ionospheric conditions using a stored transmission-frequency model, determines a future optimum working frequency and switch time, and transmits at that frequency.

**OceanMail design-around:** preserve PR-7. Keep the shared propagation dataset architecture distinct from a Station that independently fuses multiple skywave telemetry streams into a predictive working-frequency model.

**Review trigger:** receiving multiple over-HF propagation/telemetry feeds and fusing them locally to select the future working frequency.

### MEDIUM engineering attention

#### US10116382B1 — Ad hoc high frequency network — Rockwell Collins

Screening status: active; Google Patents lists adjusted expiration 2037-04-30.  
Source: https://patents.google.com/patent/US10116382B1/en

Claim 1 combines network-synchronized time, BLOS reflective communications on a TDMA waveform, and periodic broadcast of a location update on every frequency in a pick list, including information about the device and its direct-connection neighbors.

**OceanMail design-around:** preserve PR-5. OceanMail leases/announced windows do not require a globally synchronized TDMA RF network, and route advertisements should not periodically flood location plus direct-neighbor topology on every candidate frequency.

#### US10693683B1 — Systems and methods for resilient HF linking — Rockwell Collins

Screening status: active; Google Patents lists anticipated expiration 2039-07-23.  
Source: https://patents.google.com/patent/US10693683B1/en

Claim 1 uses an HF connection request and acknowledgement followed by a predefined data load known to the receiver; the receiver estimates wideband-channel parameters and returns them; the sender chooses a data rate based on those estimates.

**OceanMail design-around:** preserve PR-10. Do not implement the training/load/rate-selection sequence at Station level.

#### US8311488B2 / EP2418892B1 — HF ALE with wideband probe — L3Harris/Harris

Screening status: US active; Google Patents lists adjusted expiration 2030-12-31.  
Source: https://patents.google.com/patent/US8311488B2/en

Independent claims establish a narrowband ALE link, send a wideband probe, derive channel characteristics from that probe, return/report those characteristics, and update the narrowband link based on them.

**OceanMail design-around:** preserve PR-10 and the upstream-first boundary.

#### US9008594B2 — Method and system of adaptive communication in the HF band — Thales

Screening status: active; Google Patents lists adjusted expiration 2032-09-06.  
Source: https://patents.google.com/patent/US9008594B2/en

Claim 1 dynamically selects a set of equal-width channels at the receiver based on allocation and quality, changes band if too few qualify, reports the result to the transmitter, and simultaneously transmits on the determined number of channels.

**OceanMail design-around:** preserve PR-11.

#### US11678372B1 — Hidden-node collision avoidance in 4G ALE — Rockwell Collins

Screening status: active; Google Patents lists anticipated expiration 2041-11-29. European family includes EP4188024A1.  
Source: https://patents.google.com/patent/US11678372B1/en

Claim 1 is specific to an ALE linked call with transmit/receive sub-channel vectors and collision-avoidance PDUs sent during scan dwell, carrying node ID, priority, maximum call duration, and transmit/receive identifiers.

**OceanMail design-around:** preserve PR-12. Keep Band 0/Band 1 application-level coordination distinct from 4G-ALE sub-channel-vector collision avoidance.

### WATCH / lower-layer-specific

#### US11395353B2 / EP3855863B1 — 4G ALE protocol enhancement — Rockwell Collins

Screening status: US active; Google Patents lists adjusted expiration 2040-10-25.  
Source: https://patents.google.com/patent/US11395353B2/en

The independent claim uses a specific multi-PDU 4G-ALE handshake with Transmit Level Control blocks, several SNR values, and a stored lookup table.

**OceanMail direction:** do not implement this handshake in Station. Treat 4G ALE as upstream radio/modem behavior subject to separate supplier/license review.

#### US11425605B1 — ALE asymmetric-link sub-channel alignment — Rockwell Collins

Screening status: active; Google Patents lists anticipated expiration 2040-12-31.  
Source: https://patents.google.com/patent/US11425605B1/en

The claims concern WALE links with even/odd sub-channel counts, half-subchannel frequency misalignment, and equipment-capability signaling.

**OceanMail direction:** do not implement this link-layer mechanism in Station.

#### US11190862B1 / EP4002927B1 — Enhanced HF avalanche relay protocol — Rockwell Collins

Screening status: US active; Google Patents lists anticipated expiration 2040-11-16.  
Source: https://patents.google.com/patent/US11190862B1/en

The claims define synchronized primary/relay windows for voice, situational-awareness, and control traffic.

**OceanMail direction:** current mail/control bands are scheduler categories, not this TDM waveform. Re-review if Emergency evolves into fixed network-wide relay windows.

#### US8565164B2 — Wireless mesh architecture

Screening status: active; Google Patents lists expiration 2027-08-09.  
Source: https://patents.google.com/patent/US8565164B2/en

The independent claims use particular rendezvous-duration negotiation and adjacency-vector/channel-density mechanisms.

**OceanMail direction:** do not adopt those specific algorithms. Remaining term is comparatively short, but status must still be checked while active.

#### EP2223480B1 — Electronic mail system over a radio link

Screening status: European patent; Google Patents lists anticipated expiration 2028-11-18.  
Source: https://patents.google.com/patent/EP2223480B1/en

The claims are tied to a specific HF-email arrangement involving domain/callsign mapping, ALE frequency selection, return-receipt behavior, and STANAG 5066.

**OceanMail direction:** preserve native OceanMail Station identity/service routing and the centralized Internet-mail boundary rather than implementing that claimed combination. Recheck validated national status before European deployment.

## Recommended baseline for future HF implementation

The following is the conservative OceanMail baseline to carry into the Station implementation unless later evidence or legal review justifies something different:

1. **Legal channel catalog:** signed/versioned region/service-aware candidate channels.
2. **Rendezvous:** one configured/deterministically selected rendezvous channel or bounded set; compact presence/contact signaling.
3. **No spectrum-harvesting protocol in OceanMail:** Station does not continuously build an unused-spectrum map from peer probes to negotiate working frequencies.
4. **Working channel:** deterministic choice from the legal candidate set, simple pairwise agreement, or separately reviewed upstream ALE.
5. **No location in frequency negotiation:** location may exist for user/product features, but not as a required input/field in the OceanMail link-frequency proposal.
6. **Route advertisement:** gateway/destination reachability + scalar metric/freshness/willingness; no complete neighbor matrix exchange.
7. **Relay:** one selected next-hop custody transfer at a time; no synchronized cooperative retransmission by all listeners.
8. **Propagation:** authoritative shared forecast/profile and local historical evidence may influence when/which profile to try, without fusing multiple received skywave telemetry streams into OceanMail's own future-frequency predictor.
9. **Frequency model:** no claimed desired-power/interferer-power/LUF/MUF/sensitivity discard algorithm.
10. **Relay choice:** choose existing reachable Stations from observations/advertisements; do not solve for an ideal relay position from modeled link deficit.
11. **Link adaptation:** modem/radio owns probes, SNR/BER-based rate adaptation, FEC/ARQ, and ALE mechanics.
12. **Emergency:** application-level priority, authenticated coordination, bounded responder suppression/backoff, and pairwise custody; no avalanche PHY/MAC protocol.
13. **Single working RF opportunity:** baseline pairwise exchange uses one negotiated working channel; no OceanMail-owned simultaneous multi-channel aggregation.

## Mandatory review triggers

A new patent review is required before implementation if a proposal introduces any of these:

- peer channel-quality probes on a beacon/rendezvous channel;
- a spectrum-occupancy/unused-frequency database;
- smart link counter-proposals based on peer quality metrics;
- node location included in working-frequency negotiation;
- periodic exchange or merging of neighbor/connectivity matrices;
- network-wide synchronized TDMA RF operation;
- location + direct-neighbor broadcasts on every frequency in a pick list;
- coordinated retransmission of the same signal/message by two or more relay Stations;
- avalanche/flooded call-and-response link establishment;
- fixed relay windows for all Stations;
- wideband/chirp training probes controlled by OceanMail;
- choosing bitrate from a receiver-returned channel-estimate report;
- fusing two or more skywave-received telemetry streams into a frequency prediction model;
- explicit desired-signal versus interferer received-power modeling per candidate frequency;
- geometric relay-position computation from link deficit;
- simultaneous aggregation of several HF working channels;
- custom 4G-ALE TLC/SNR or sub-channel-vector collision-avoidance mechanisms.

## Upstream/vendor due diligence

Before OceanMail ships or recommends a modem/radio feature that falls into one of the areas above:

1. identify exactly which component implements it;
2. record component version and supplier/upstream project;
3. determine whether the feature is part of a standard, proprietary implementation, or open-source implementation;
4. review any express patent license or patent grant in that component's license;
5. do not assume an open-source copyright license automatically clears third-party patents;
6. for commercial hardware/software, check the supplier's license/right-to-use and applicable indemnity terms;
7. do not copy claim language or patented implementation detail into OceanMail merely to reproduce a feature already available below the Station boundary.

## Jurisdiction and release gate

Patent rights are territorial. A U.S.-focused claim review does not clear operation or sales in Europe, Canada, Australia, or other maritime markets.

Before:

- physical-radio Phase 5 becomes a release/product capability;
- OceanMail sells or distributes a Station configured for automatic HF operation; or
- a major new routing/rendezvous algorithm is frozen for production,

obtain a targeted freedom-to-operate review using the final implementation and intended jurisdictions. That review should:

- verify current status in official patent registers;
- claim-chart the final design against the HIGH-attention families above;
- search continuations/divisionals and patents issued after this review date;
- check international family members in target markets;
- review upstream modem/radio patent rights; and
- confirm that any intentional design-around remains materially outside the asserted claim combinations, including equivalents.

## Relationship to current OceanMail documentation

This register is consistent with:

- `PROJECT.md` — upstream-first and evidence-gated complex networking;
- `docs/decisions/ADR-004-station-store-transport-grid-control.md` — separation of Station Grid/control from store/transport;
- `docs/decisions/ADR-008-four-band-scheduling-and-channel-use.md` — rendezvous, pairwise directed exchange, single-radio baseline, and unfinished Emergency access protocol;
- `docs/specifications/communications-foundation-positioning.md` — do not recreate modem/ALE/ARQ behavior when upstream satisfies the requirement;
- `OceanMail/oceanmail-station/docs/research/RADIO_RENDEZVOUS_AND_LINK_REQUIREMENTS.md` — ALE-style work remains research and lower-layer reliability remains upstream-owned.

This document does **not** authorize physical-radio testing or modify existing regulatory gates.
