# OceanMail Decision Ledger

> Publication scope update — 2026-09-26: the owner approved fresh public repositories for **all five active components: Project, Station, Desktop, Server and Infrastructure**. Preserve the original repositories privately with `-archive` suffixes. The five older BEMPIC/0.1 repositories remain private and frozen. Earlier three-repository scope statements below are superseded historical records.


> Current publication decision (2026-09-26): create fresh sanitized Project, Station and Desktop repositories with installed licenses. Preserve the original repositories privately under names ending in `-archive`. See [PUBLICATION.md](PUBLICATION.md). Earlier in-place conversion instructions and pending-license statements below are historical.


This ledger is the inexpensive place to preserve small-to-medium project decisions and clarifications. Significant architecture decisions receive an ADR under `docs/decisions/`.

## 2026-09-26 — Earlier narrowed publication scope (superseded)

**Owner direction (2026-09-25):** only Project, Station and Desktop are being prepared for publication, in that priority order. Server and Infrastructure remain private. This supersedes the earlier five-repository publication scope, while privacy/document review remains organization-wide. Archived repositories remain historical; no development restart is authorized.

## 2026-09-26 — Publication privacy disposition and approved choices

**Owner direction (2026-09-25):** remove personal data and private runner information before publication. Review all ten organization repositories, including frozen archives. Current-file redaction alone does not satisfy the history, GitHub-surface, log/artifact or cached-copy gates. Keep active repositories private until all gates pass. Preserve restricted recovery evidence and third-party attribution; no unrelated historical feature development is authorized.

**Approved:** AGPL-3.0-only for OceanMail-owned code; CC-BY-SA-4.0 for documentation, subject to rights/compatibility review. Required approving review count is zero, with PRs, required checks and maintainer-only merges still required. These choices do not assert that license files/settings are applied. DCO/inbound contribution terms and authority over existing contributions remain separate unresolved items.

**Execution boundary:** current-file and discussion cleanup can proceed through supported repository operations. Full history/identity rewriting, GitHub-managed refs/caches, archived-repository edits and retained artifact/log removal require appropriate authenticated Git/admin access. No complete erasure or publication clearance is claimed.

## 2026-09-25 — Public fork/PR collaboration and defensive publication

**Status:** Collaboration policy retained; five-repository publication scope superseded by the narrowed scope above.

Prepare Project, Station, Server, Desktop and Infrastructure for public access in that order. Outsiders, including Rafael, normally contribute through forks/PRs without write access. Maintainers control merges; retain merge commits and rollback history. Use standard GitHub-hosted public PR CI; exclude public repositories from trusted self-hosted runners and local workstations at the runner access boundary.

No patents by default. Prefer technically meaningful open/defensive publication, preserving prior-art and upstream attribution. License/contributor terms and historical privacy disposition remain pending. The owner authorized preparation and safe completed-work merges; this does not waive publication gates or grant a license.

See [public collaboration policy](docs/specifications/public-collaboration.md), [pending decisions](docs/specifications/publication-decisions.md), and [master issue #42](https://github.com/OceanMail/oceanmail-project-archive/issues/42). This supersedes earlier uncertainty about whether the five active repositories should be prepared for public contribution; it does not claim they have become public or that sensitive operational material may be exposed.

## 2026-09-22 — Personal mail control in Band 2 and encryption boundaries

**Decision:** Band 1 is public discovery/route/access coordination plus authorized urgent public updates. Band 2 includes ordinary manifests, requests, receipts, custody/repair/stop-flow/tombstones, account reconciliation, and payload, with expedited mail control within its fairness shares. Bands 0/1/3 are public over HF. Client–own Station, direct Client–Server Internet, and gateway–Server connections are always authenticated and encrypted. Personal HF encryption, if adopted, terminates at Station and Server through untrusted relays/gateways; the deployed path has no plaintext capability or fallback. A single deployment choice remains pending feasibility, not a user or per-message option. External SMTP is a separate boundary without a universal encryption guarantee.

**Status:** ACCEPTED DESIGN; implementation/security validation remains outstanding. Native direct-delivery key boundaries remain unresolved without changing decentralized availability or permitting a plaintext exception. See [ADR-009](docs/decisions/ADR-009-personal-traffic-and-encryption.md).

## 2026-09-21 — Four bands, capped control, and shared broadcasts

**Placement amended by ADR-009 on 2026-09-22:** the following records the original classification; ordinary mail metadata/control now belongs in Band 2.

**Original decision:** Band 0 is Emergency and its own control/propagation; Band 1 is control/manifests/Grid coordination and authenticated Server-designated urgent updates; Band 2 combines local-account and third-party relay payload; Band 3 is shared background broadcast data.

**Lease:** Duration and normal Band 1 allowance are independent tuning inputs. The owner's 2026-09-21 clarification makes ten/four minutes arithmetic examples, not defaults or a fixed 40% ratio. Operating values await measured transport and responsiveness evidence. Band 1 may use the full lease for necessary route establishment, yields at expiry, and returns to its configured normal cap once a route exists. Band 2 uses remaining time. Band 3 has no reserved lease share; use idle opportunities or announced broadcasts when updates exist. Release unused leases early. Emergency preempts ordinary work/budgets while preserving existing authorization gates.

**Fairness and channels:** Band 2 retains local-account and per-Station relay fairness and bounded acceptance against forwarding backlog. Use rendezvous announcements, negotiated addressed Band 1 then Band 2 on the same exchange channel, and time/channel/dataset/version/duration announcements for shared broadcasts. Single-radio listening/check-in and Emergency preemption require bounded validated mechanisms. Passive reception does not grant custody or private-account access.

**Supersession:** Replaces the earlier six-band draft, the 2/6/2 reserved-slot proposal, and the blanket no-full-lease-ordinary-band rule, all preserved in PR/commit history. Also supersedes Decision 0009's old five-band hierarchy. User/ship byte budgets and Station airtime budgets remain capacity controls; initial durations/caps and fairness weights remain tunable.

**Status:** ACTIVE DESIGN; implementation outstanding. See [ADR-008](docs/decisions/ADR-008-four-band-scheduling-and-channel-use.md).

## 2026-09-14 — HF link-capacity tiers and survival mode

**Decision:** OceanMail schedules constrained-link work using progressive delivered-throughput tiers across an initial design range of approximately 0.1–3 kbps. Links below 0.1 kbps enter survival mode, where payload-size and relay costs rise sharply, deferrable/background traffic is normally suppressed, and the Station minimizes airtime while preserving safety, delivery progress, repair, and recovery traffic.

**Clarification:** Survival mode is not local-only and does not absolutely prohibit relay. High-value relay work may remain eligible when withholding it would materially reduce delivery probability, but Emergency eligibility never bypasses the existing technical-capability and legal/operational-permission gates. Capacity tiers and an Emergency label do not independently authorize transmission, unattended operation, or store-and-forward relay.

**Reason:** A binary usable/unusable model either wastes scarce airtime or strands small, valuable traffic when propagation is poor. Progressive cost and eligibility preserve useful delivery behavior without turning a degraded Station into a bulk transit carrier.

**Affected components:** Station scheduler; GRID / CONTROL relay and route selection; STORE / TRANSPORT execution/accounting; compact control, manifest, receipt, tombstone, and reconciliation formats.

**Status:** ACTIVE. See ADR-007.

## 2026-09-11 — Dedicated OceanMail GitHub organization and explicit repository names

**Decision:** OceanMail repositories live under the dedicated `OceanMail` GitHub organization rather than using another project organization as an umbrella merely to share infrastructure. Active component repositories use descriptive names such as `oceanmail-desktop`, `oceanmail-station`, `oceanmail-server`, and `oceanmail-infrastructure`.

**Clarification:** `OceanMail/oceanmail-desktop` is intentionally named for the Desktop component. A generic active repository named `OceanMail/oceanmail` would be ambiguous with the overall project/organization and is not the current naming model.

**Reason:** OceanMail is an independent multi-repository product/ecosystem with its own collaboration, permissions, publication, Actions, secrets, and contributor boundaries. Clear component names reduce ambiguity as the organization grows.

**Rejected/Previous behavior:** placing OceanMail under another project organization solely to share runners, or retaining the active Desktop repository as generic `oceanmail`.

**Affected components:** all OceanMail repositories and organization administration.

**Status:** ACTIVE.

## 2026-09-11 — Self-hosted CI runners are organization-scoped shared infrastructure

**Decision:** OceanMail self-hosted GitHub Actions runners should normally be registered at the `OceanMail` organization scope and shared with authorized active repositories, rather than being owned by one repository and repeatedly reconfigured as work moves between repositories.

**Clarification:** Runner-group and repository access controls must exclude public repositories and untrusted fork code from trusted self-hosted execution. Workflow conditions and VM snapshots are not substitutes for this boundary. Public validation now uses GitHub-hosted runners.

**Status:** Policy retained; private operational identities/configuration removed from this publication-facing record by owner direction. Administrative exclusion still requires verification. See `OceanMail/oceanmail-infrastructure/docs/CI-RUNNERS.md` for public security requirements.

## 2026-09-11 — Organization-level project spine

**Decision:** `OceanMail/oceanmail-project` is the authoritative home for organization-level definition, architecture, terminology, repository inventory, cross-repository decisions, current project state, workstream orientation, and AI/contributor operating rules.

**Clarification:** Component repositories remain authoritative for their source code and component-specific implementation documentation.

**Reason:** Long-running AI/chat context is disposable and cannot be the durable source of project truth.

**Rejected/Previous behavior:** `oceanmail-desktop/docs` previously claimed program-level cross-repository authority.

**Affected components:** all OceanMail repositories.

**Status:** ACTIVE. See ADR-001.

## 2026-09-11 — AI/contributor role convergence

**Decision:** Owner remains final decision-maker. ChatGPT is primary architecture/system-design/planning/coordination lead. Codex is primary implementation/coding agent. Claude is a supporting architecture/review agent and independent critic. Git/GitHub is the durable convergence point.

**Clarification:** Codex is the default agent for actual repository implementation work and normally operates from the Linux client/bash environment. Claude may provide proactive advisory critique when useful, including when ChatGPT asks it to review an architectural decision for risks, alternatives, missing considerations, or improvements. Claude is not a competing architecture authority or mandatory approval layer; ChatGPT remains the primary designer and decides which Claude suggestions, if any, are incorporated into project direction or implementation instructions.

**Reason:** Multiple agents are useful only if decisions converge into one durable source of truth and architecture ownership remains unambiguous.

**Rejected/Previous behavior:** agent-specific project truth, chat-only architectural continuity, or treating Claude/Codex output as an independent architecture authority.

**Affected components:** all.

**Status:** ACTIVE. Detailed workflow: `docs/specifications/ai-development-workflow.md`.

## 2026-09-11 — Desktop Mail hierarchy and queue ownership

**Decision:** Each OceanMail Desktop account presents the Mail hierarchy `Inbox / Available / Saved / Drafts / Sent / Trash`. There is no user-facing OceanMail Outbox.

**Clarification:** `Available` is an account-scoped remote-manifest/pseudo-folder view, not IMAP. `Saved` is a real mailbox/folder where supported. `Sent` is native Sent augmented only with truthful authorized Station evidence when securely correlated. `Trash` is the account's normal IMAP `\Trash` special-use folder and is expected; it is not an Outbox substitute. After ordinary mail is durably handed to the accepted Station/mail-submission boundary, persistent queueing, retry, constrained-link execution, and transport/receipt evidence belong to Station/store-transport state rather than to a Desktop-owned Outbox queue.

**Reason:** Thunderbird's native Local Folders/Outbox artifact and older OceanMail prototype terminology can falsely imply that Desktop owns constrained-link queue state or that a local queue state proves remote progress. The accepted model keeps familiar mailbox concepts while preserving truthful Station evidence semantics.

**Rejected/Previous behavior:** a user-facing OceanMail Outbox and any UI model that treats Thunderbird/local queue state as the authoritative constrained-link transport queue.

**Affected components:** Desktop; Desktop↔Station evidence/status boundary; future account-scoped Station APIs.

**Status:** ACTIVE. Detailed Desktop implementation truth remains in `OceanMail/oceanmail-desktop`.

## 2026-09-11 — Station deployment, local WLAN, and hard-power-loss requirements

**Decision:** OceanMail-operated permanent gateways use the same Station software as vessel Stations. Station hardware may use different reference profiles: low-power passive ARM64 for owner/vessel appliances and fanless x86-64/thin-client/N100-class hardware for permanent institutional gateways. A Station-provided Wi-Fi network is an OMail/OChat/management service network only, not a NAT/general Internet router. Routine abrupt power removal must be supported as normal marine operation, with automatic crash-safe recovery and resume on power restoration.

**Clarification:** Wi-Fi may operate as local AP, upstream client, or proven concurrent AP+STA where hardware permits; a second USB Wi-Fi adapter is acceptable. Do not assume concurrent AP+STA from a specific SBC without qualification. Durable storage quality matters more than large capacity; permanent Internet-connected gateways are transit nodes with bounded queues/logs/cache.

**Reason:** Vessel installations may have only switched DC power and Wi-Fi-only Starlink/marina connectivity, while permanent shore gateways favor serviceability and durability over minimum watts.

**Affected components:** Station, Infrastructure, hardware qualification, client discovery/management.

**Status:** ACTIVE design requirement. See `docs/specifications/station-deployment-power-networking.md`.

## 2026-09-11 — Hosted backend is logically decomposed but initially co-deployable

**Decision:** Hosted OceanMail functions are independent logical services with explicit APIs/data ownership, but may initially run together on one VPS or a small number of VPSs. Service domains include Internet-mail conversion, account/identity/auth, encrypted telemetry/log analytics and reputation/abuse processing, Grid coordination/data publishing, software health/update/config/data distribution, and internal administration.

**Clarification:** Native OMail transport/store-and-forward remains Station-owned and decentralized. Hosted Grid services aggregate/coordinate/publish selected authoritative data; they are not a mandatory real-time transport/routing engine. Telemetry is structured operational evidence used for reputation, contribution, abuse/AUP, reliability, network health, and statistics, not merely debug logging.

**Reason:** Preserve autonomous Station behavior while allowing hosted functions to scale independently without redesign.

**Affected components:** Server, Station, Infrastructure, Grid/control.

**Status:** ACTIVE architectural direction. See `docs/architecture/backend-service-decomposition.md`.

## 2026-09-04 — Public Internet mail is centralized; native OMail is not

**Decision:** OceanMail-operated Server/infrastructure is the sole public Internet SMTP/MX boundary. Internet-connected Stations and gateway Stations do not deliver directly to arbitrary public SMTP systems and are not independent public Internet MTAs.

**Clarification:** This centralization applies only when traffic crosses between native OMail and conventional public Internet mail/services. Native boat-to-boat/store-carry-forward OMail remains decentralized and must continue without Internet or central Server availability. A central outage may delay and queue/retry Internet-boundary work but must not disable viable native OMail paths.

**Reason:** Centralizing reputation, DKIM/SPF/DMARC, destination retries, bounce handling, abuse controls, and public-mail operations reduces Station complexity and trust surface without sacrificing native OMail capability.

**Rejected/Previous behavior:** direct public SMTP delivery from gateway Stations or privileged per-Station access to a central public-mail smarthost.

**Affected components:** Server, Infrastructure, Station gateway behavior, Desktop delivery semantics.

**Status:** ACTIVE. See ADR-006.

## 2026-09-11 — Station STORE/TRANSPORT and GRID/CONTROL separation

**Decision:** OceanMail Station has a logical **STORE / TRANSPORT Plane** and **GRID / CONTROL Plane** joined through Station-owned core identity/configuration/API/event/state boundaries. GRID / CONTROL decides network behavior and policy; STORE / TRANSPORT coordinates authoritative stores/transports, executes accepted work, and reports measurable evidence.

**Clarification:** Relay and gateway policy, peer/topology observations, reputation/telemetry inputs, map/network state, and OChat Grid behavior belong to GRID / CONTROL. HERMES, Mercury, Taylor UUCP, Postfix, Dovecot/mailbox storage, ordinary IP, and later accepted adapters remain STORE / TRANSPORT responsibilities and must not absorb OceanMail Grid policy merely because they hold or move bytes. The split is logical and does not require separate processes or machines.

**OChat:** OChat is ephemeral GRID / CONTROL behavior using shared STORE / TRANSPORT resources; it is not durable OMail store-and-forward traffic. OMail may preempt OChat, eager/reluctant relay modes do not govern ordinary OChat forwarding, and OChat airtime/resource policy remains separate.

**Reason:** Keep OceanMail network intelligence/policy independent from upstream transport/store implementations and allow transport evolution without changing Grid semantics.

**Rejected/Previous behavior:** embedding OceanMail relay/gateway/OChat/routing policy into lower-layer transport components, or treating OChat as durable mail because it shares radio/IP resources.

**Terminology:** the original September 4 name `Mail / Transport Plane` was broadened to `STORE / TRANSPORT Plane` to include authoritative durable store/queue coordination and evidence.

**Affected components:** Station, Desktop/management surfaces that expose Station state, Server/gateway policy, future Grid services.

**Status:** ACTIVE. See ADR-004 and `OceanMail/oceanmail-station/docs/OCEANMAIL_0_2_PRODUCT_STATION_DECISIONS.md`.

## 2026-09-11 — Relay and gateway mode semantics retained from current Station authority

**Decision:** While a Station is running there is no relay `Off` mode. Relay behavior is **Eager** or **Reluctant**. Eager relays advertise availability and may be selected normally, subject to Station resource controls. Reluctant relays do **not** advertise; they listen and may intervene as fallback for Emergency or stranded/stalled Ordinary traffic when accepted Grid policy determines help is warranted.

Gateway policy is independent of relay willingness and uses **Full**, **Minimal**, and **Off** for ordinary third-party gateway service:

- **Full** normally offers ordinary third-party gateway service.
- **Minimal** normally does not, but may provide fallback for stranded/stalled Ordinary traffic when no suitable Full Gateway/route exists or excessive delay has accumulated.
- **Off** offers no ordinary third-party gateway service.
- **Emergency** remains eligible in all gateway modes when the Station is technically capable and legally/operationally permitted to assist.

**Clarification:** Reluctant is silent fallback behavior, not an advertised low-preference relay. Minimal is fallback-oriented, not equivalent to Off. `Important` metadata and credits do not affect relay precedence or gateway/path selection.

**Superseded detail:** the September 4 `Minimal/Priority Gateway` idea depended on an ordinary sender-selectable Priority class. The later Emergency/Ordinary decision removed that class, so current Minimal behavior uses route failure/stall/accumulated delay for Ordinary traffic rather than Priority labeling.

**Reason:** Preserve current Station/Grid semantics, keep relay and gateway willingness orthogonal, and prevent old 0.1/early-0.2 mode names or Priority-era assumptions from being reintroduced.

**Rejected/Previous behavior:** relay `Off` while the Station is running; advertising Reluctant relays as merely lower-priority relays; Priority-only Minimal Gateway semantics.

**Affected components:** Station, Desktop status/controls, Grid/control, Server/gateway policy.

**Status:** ACTIVE; implementation remains incomplete. See ADR-004 and Station component documentation for detailed current semantics and legal/operational qualifications.

## 2026-09-06 — Emergency/Ordinary replaces ordinary transport Priority

**Decision:** Emergency is the only user-originated mail class that changes transport precedence. Ordinary mail may be marked `Important`, but that is metadata only. Recipient ordering of Available mail is retrieval intent within ordinary work, not a new RF priority class.

**Reason:** Sender-selectable ordinary Priority predictably collapses into overuse and can crowd shared constrained capacity.

**Rejected/Previous behavior:** 0.1 Normal/Priority ordinary transport classes where they conflict.

**Affected components:** Desktop, Station scheduler, accounting/policy, Available.

**Status:** ACTIVE. Original rationale remains in Desktop Decision 0009 pending historical decision migration/indexing.

## 2026-09-04 — Visual identity direction: integrated `O` mark and wordmark

**Decision:** The current OceanMail visual-identity direction is a simple integrated wordmark using the deep-navy plus cyan/teal palette. The standalone symbol also replaces the initial `O` in `OceanMail`: a simple `O`/globe/ocean form crossed by one letter/envelope/sail-like swoosh. The `M` in `Mail` is intended to become an envelope-derived glyph occupying the same typographic footprint as the normal `M`.

**Clarification:** Final artwork is not approved. For the envelope-derived `M`, the envelope itself must form the letter: its left/right outer edges are the `M` stems and the bottom edge of the envelope flap supplies the inward diagonals/central valley. An ordinary `M` with a chevron, notch, or envelope decoration does not satisfy the requirement.

**Reason:** The brand should be immediately recognizable, memorable at small sizes, simple enough to work in one color, and maritime/mail-oriented without becoming a literal multi-icon illustration.

**Rejected/Previous behavior:** complex globe/sail/wave/network illustrations; face/lips-like wave compositions; literal globe grids; exaggerated retro display type; and treating the earlier 1970s/1980s, Art Deco, or Streamline/Loewy explorations as final direction.

**Affected components:** organization branding, Desktop packaging/UI, web/public identity, documentation, and future brand assets.

**Status:** ACTIVE DESIGN DIRECTION; final geometry, type, exact colors, vector masters, and trademark/similarity review remain unresolved. See `docs/specifications/visual-identity.md`.

## 2026-09-03 — HERMES/Mercury upstream-first communications foundation

**Decision:** OceanMail 0.2 uses HERMES-derived store/transport behavior with Mercury as the preferred open HF modem baseline. Additional transports remain behind the Station boundary.

**Reason:** Avoid rebuilding lower-layer communications work already maintained upstream and reach real testing sooner.

**Rejected/Previous behavior:** mandatory clean-sheet OceanMail -> BEMPIC -> M4P -> DataLink stack.

**Affected components:** all communications architecture.

**Status:** ACTIVE. See ADR-002.

## 2026-09-02 — BEMPIC frozen; M4P tabled for OceanMail 0.2

**Decision:** BEMPIC development is frozen and M4P integration is tabled for the active OceanMail path.

**Clarification:** BEMPIC is preserved as independent research and may resume only if comparative evidence justifies the added protocol/maintenance burden. M4P remains an external reference design, not an OceanMail dependency or a layer beneath/alongside HERMES/Mercury.

**Boundary:** HERMES/Mercury/Taylor UUCP owns the active STORE / TRANSPORT baseline. It does not itself provide OceanMail's future public-network identity, federation, service/gateway discovery, relay selection, reputation, or opportunistic-routing policy; those concerns remain evidence-gated GRID / CONTROL work above the transport boundary.

**Evaluation rule:** Later M4P specification improvements do not automatically reopen this decision. Reconsider integration only through a deliberate architecture decision backed by an accessible implementation, a workable answer for the required interoperability/federation scope, and comparative RF/field evidence showing a missing capability or material advantage over the HERMES/Mercury baseline.

**Reason:** HERMES/Mercury provides a functioning baseline that must be measured before another store-forward, fragmentation, receipt, or scheduling layer is added. Parallel lower-layer machinery would duplicate responsibility and evidence semantics.

**Affected components:** BEMPIC, historical 0.1 stack, Station STORE / TRANSPORT, future GRID / CONTROL.

**Status:** ACTIVE program decision; BEMPIC itself is FROZEN.

