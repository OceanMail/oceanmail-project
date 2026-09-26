# OceanMail Shared Terminology

Status: CURRENT

- **OceanMail Desktop** — current desktop client product, built on a pinned Thunderbird foundation.
- **OceanMail Station** — persistent onboard/edge communications service that may run headless and serve multiple clients.
- **OceanMail Server** — hosted Internet-side application/service boundary.
- **OMail** — native OceanMail message/mail semantics; not synonymous with conventional Internet email or an external service such as Winlink/SailMail.
- **Grid** — user-facing term for OceanMail's constrained/intermittent communications environment and the Station observations/control state associated with it. Use `Grid` in product UI and current documentation rather than introducing a separate `OceanNet` network brand. `Grid` does **not** imply that OceanMail requires or already implements a global multi-hop mesh; direct Station/gateway/service operation is valid and multi-hop remains evidence-gated.
- **Logical OMail message ID** — durable application identity for one OMail message across retries, lower-layer job-ID changes, relay handoffs, and later repair attempts. An RFC `Message-ID` may be correlation evidence but is not sufficient authorization or globally trustworthy logical identity by itself.
- **Available** — private account-scoped metadata describing content held elsewhere before constrained-link payload retrieval; not an IMAP folder and not already-local message content.
- **Delivery receipt** — returned evidence that the applicable authoritative destination has durably accepted/stored the message to the level claimed. It is not the same as transport/session success, an intermediate relay handoff, or proof that a human read the message.
- **Delivery tombstone** — compact, longer-lived record that a logical message has already reached its authoritative destination, retained to suppress stale re-injection after larger payload/cache state has expired.
- **Relay responsibility** — future Grid/control state in which a Station agrees to actively attempt to advance eligible traffic. It is not final-delivery evidence and does not automatically require the source or other holders to delete their copies. Multi-hop execution remains evidence-gated.
- **Emergency** — exceptional user-originated traffic class that may change transport precedence under accepted safeguards/policy.
- **Ordinary** — normal user mail traffic. There is no current sender-selectable ordinary transport Priority class.
- **Important** — conventional/interoperable message metadata. It does not buy or grant RF/Station/relay precedence, gateway/path preference, credits, or quota class.
- **STORE / TRANSPORT Plane** — Station term for durable holding/movement of accepted traffic and transport/receipt evidence.
- **GRID / CONTROL Plane** — Station term for Grid observations, topology, relay/gateway policy, telemetry/reputation inputs, OChat Grid behavior, and future selection/routing intelligence.
- **Eager relay** — relay mode that advertises/volunteers broadly subject to resource controls.
- **Reluctant relay** — non-advertising/fallback relay behavior for Emergency or stranded/stalled ordinary work according to accepted policy; not relay Off.
- **Full Gateway** — normally offers ordinary third-party gateway service.
- **Minimal Gateway** — normally does not offer ordinary third-party service but may be used by accepted Grid fallback policy for stranded/stalled ordinary traffic.
- **Gateway Off** — no ordinary third-party gateway service; Emergency may remain eligible when technically, legally, and operationally permitted.
- **OMGP** — historical clean-sheet OceanMail protocol concept for a worldwide, multi-modal, independently administered maritime grid. Its requirements may inform future GRID / CONTROL work, but OMGP is not a current protocol, dependency, or synonym for the current GRID / CONTROL plane.
- **BEMPIC** — frozen protocol research for compact/interruption-tolerant application synchronization; not an active mandatory OceanMail 0.2 layer.
- **M4P** — external Multi-Modal Maritime Mesh Protocol researched during OceanMail 0.1. It is tabled for 0.2 and may be used as prior art; it is not an active dependency or the current OceanMail transport architecture.
- **HERMES/Mercury** — current upstream-first constrained-communications foundation used by Station integration.
