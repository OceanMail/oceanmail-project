# Scheduling documentation audit — 2026-09-21

Scope: scanned 278 repository-owned Markdown/reStructuredText/text files during the pre-publication documentation review (vendor trees excluded). Reviewed matching scheduling/band references and relevant Emergency, shared-update, channel, accounting, authority, and historical-status documents. This is a documentation audit, not a code or protocol correctness review.

## Public component source snapshots (historical subset)

| Repository | Source commit | Files scanned |
| --- | --- | --- |
| oceanmail-project | `ac82516943f9d9bf6a7d9dd752ac98c5c8b8722a` | 45 |
| oceanmail-station | `a06811170455e91c6ec04e847d0eb69ced78bdcb` | 22 |
| oceanmail-desktop | `23a412493515f7513c25e43af46448f74118c86f` | 56 |
| oceanmail-server | `23a1c39a40734e4d4eaccd8555fafd388d335963` | 3 |
| oceanmail-infrastructure | `228b6d3602d39843eefce1c3aba454e1a6c0f90b` | 4 |

Project/Station/Desktop source snapshots are the existing documentation PR heads; other repositories use their observed main heads.

## Findings and disposition

- **Project:** revise ADR-008 and rename it to [four-band scheduling and channel use](../decisions/ADR-008-four-band-scheduling-and-channel-use.md); reconcile ledger, decision index, current-state scheduling section, accounting, Station/Server workstreams, and backend publishing responsibility.
- **Station:** reconcile architecture, Available numbering, status, accounting, and index; connect rendezvous/single-radio research to accepted activity-based channels while keeping frequencies, protocol implementation, and RF proof unresolved.
- **Desktop:** reconcile scheduling/metering and API documents; preserve Decision 0009's original hierarchy as explicitly superseded history; correct current authority notices in Decisions 0004/0005/0006/0008; flag the mail-model correction's historical hierarchy; distinguish Band 0 Emergency from Server-promoted Band 1 updates in Emergency/security design.
- **Server:** add the authenticated shared-update urgency contract and Station enforcement boundary to its documentation. This is an implementation requirement, not a shipped API.
- **Infrastructure:** no conflicting scheduler/channel requirement found; existing deployment/operations boundaries remain applicable. No edit needed.
- **Five frozen/historical repositories:** existing root historical/frozen notices clearly exclude them from active OceanMail authority. Preserve their old scheduling/protocol designs as history; no active-policy edits needed.

## Preserved boundaries

Bands 0–3 supersede the unmerged six-band and 2/6/2 reserved-slot drafts. Normal Band 1 cap/route exception, Band 2 remainder, and unreserved Band 3 broadcasts are current design. Initial 10-minute leases/4-minute caps remain tunable.

The audit does not change unrelated implementation status, open validation findings, pricing, authentication/storage design, regulatory decisions, physical-radio Phase 5 gates, upstream pins, or the independent HF-tier work. Native OMail remains capable of disconnected store-and-forward operation.

No dedicated channel per band, automatic relay custody from overhearing, guaranteed passive decoding of arbitrary modem sessions, instantaneous cross-channel Emergency detection, or proven collision-free protocol is claimed.

## Validation and integration

Check Markdown whitespace/diffs, repository-path links, stale current-policy references, changed-file scope, and published PR heads. No executable changes are made; runtime/unit/integration/RF tests are not evidence for this documentation-only update.

Integrate project authority first, then its component documentation companions. Repository PRs preserve earlier drafts and the owner's later reversal in commit history.

## Merge review addendum

The integration review found an additional current-policy conflict in `delivery-evidence-and-repair.md`: ordinary receipts were still placed below local payload. ADR-008 supersedes that order; ordinary receipts/repair are now explicitly Band 1 and Emergency control remains Band 0. The snapshot date and obsolete queued/open status for the readiness and HF-tier changes were also reconciled. The Desktop scheduling-docs refreshed-head CI passed, but live Thunderbird acceptance remains open.

The two textual merge conflicts in the decision ledger and Station workstream were resolved by retaining both ADR-007 capacity-tier eligibility and ADR-008 band/channel policy. The earlier audit scope and snapshots above remain a historical record, not a claim that those were final merged heads.
