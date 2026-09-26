# OceanMail Organization Branch Retention Audit — 2026-09-11

Status: **CURRENT CLEANUP AUTHORITY**

## Purpose

This audit establishes which non-default branches in the `OceanMail` GitHub organization must be retained before historical branch cleanup. It exists to prevent accidental deletion of deliberately unmerged research, incomplete carry-forward work, or named historical-generation snapshots.

The audit covered all 10 OceanMail repositories and all 106 non-`main` branches present at the start of the audit on 2026-09-11. Pull-request history, branch ancestry, current `main`, supersession relationships, and file-level content were checked where commit topology alone was insufficient.

No existing branch was deleted during this audit.

## Retain — do not delete

The following eight branches are intentionally retained until a later explicit disposition:

| Repository | Branch | Reason |
| --- | --- | --- |
| `OceanMail/bempic` | `archive/v0.1-generation` | Explicit historical generation snapshot. No unique commits, but retained as a named historical boundary unless replaced by an immutable tag. |
| `OceanMail/bempic` | `codex/v0.1-m4p-binding-review-package` | Deliberately closed without merge when BEMPIC was frozen. Contains unique M4P binding review/research evidence that the closure explicitly preserved. |
| `OceanMail/bempic-reference` | `archive/v0.1-generation` | Explicit historical generation snapshot. No unique commits, but retained as a named historical boundary unless replaced by an immutable tag. |
| `OceanMail/bempic-reference` | `codex/v0.1-public-codec-adoption` | Deliberately closed without merge when BEMPIC was frozen. Contains unique codec/vector/conformance evidence that the closure explicitly preserved. |
| `OceanMail/oceanmail-0.1-prototype` | `archive/v0.1-generation` | Explicit historical generation snapshot. No unique commits, but retained as a named historical boundary unless replaced by an immutable tag. |
| `OceanMail/oceanmail-infrastructure-0.1-prototype` | `archive/v0.1-generation` | Explicit historical generation snapshot. No unique commits, but retained as a named historical boundary unless replaced by an immutable tag. |
| `OceanMail/oceanmail-server-0.1-prototype` | `archive/v0.1-generation` | Explicit historical generation snapshot. No unique commits, but retained as a named historical boundary unless replaced by an immutable tag. |
| `OceanMail/oceanmail-server-0.1-prototype` | `codex/server-mfa-enrollment` | Open draft PR #5 with useful unmerged TOTP/MFA security work. Exact-head PostgreSQL integration testing is still failing; this work must be repaired/revalidated before any merge or deletion. |

These are the only non-default branches found in the organization that require retention after this audit.

## Safe-cleanup result

The other **98** non-`main` branches present at audit start are safe to delete from a preservation standpoint. They fall into one or more of these classes:

- merged PR head whose content is on `main`;
- ancestor of `main` with no unique commits;
- explicitly superseded reconciliation/draft branch whose replacement was merged;
- one-time CI smoke branch whose durable evidence/procedure is recorded elsewhere;
- obsolete work branch with zero commits ahead of current `main`;
- stale reconciliation branch whose unique durable delta was separately extracted onto current `main` before this audit.

This classification is about preservation safety only. It does not require immediate deletion, and it does not change repository historical/current status.

## Squash-merge topology exceptions verified

Two historical branches appear divergent from `main` if judged only by commit ancestry because their PRs were squash-merged. File-level verification confirmed their substantive final content is already preserved on `main`:

### `oceanmail-0.1-prototype:codex/oceanmail-transfer-planner-core`

PR #5 was squash-merged as commit `64e7b7881a8b5093b43e5ed6774ae2492507b7fa`.

The final branch head and landed squash commit have identical blobs for the persistent transfer-planner source, Desktop integration source, prototype state source, and authoritative work report. The branch is therefore safe to delete despite divergent ancestry.

### `oceanmail-infrastructure-0.1-prototype:codex/infrastructure-supply-chain-acceptance`

PR #5 was squash-merged as commit `20da17b674a967eb662affe26caf5ab1bfa20b09`.

The final branch head and landed squash commit have identical blobs for the core supply-chain validator and authoritative work report, and the PR is recorded merged. The branch is therefore safe to delete despite divergent ancestry.

## Active 0.2 repositories

No unmerged implementation branch requiring preservation was found in the active 0.2 repositories (`oceanmail-desktop`, `oceanmail-station`, `oceanmail-server`, `oceanmail-infrastructure`, `oceanmail-project`).

Notable checks:

- Station `phase4j/api-auth-context-foundation` is behind current `main` with zero unique commits; actual authentication/account work remains tracked as issue #23 rather than stranded on that branch.
- The formerly unique Phase 4I lifecycle/upstream-debt material was extracted and merged through Station PR #46 and project-spine PR #32.
- The formerly unique Desktop workflow/queue/evidence material was extracted and merged through project-spine PR #33.
- Publication, Grid-accounting, RSS/News, runner, gateway, HERMES, regulatory, and other September 11 reconciliation iterations are either merged or explicitly superseded by merged replacements.

## Automatic head-branch deletion setting

At audit time, GitHub reported `delete_branch_on_merge=true` for nine of the ten OceanMail repositories.

`OceanMail/oceanmail-server-0.1-prototype` still reported `delete_branch_on_merge=false`. This does not affect the preservation classification above, but the repository setting should be corrected if future merged PR head branches there should be deleted automatically.

Do **not** delete `codex/server-mfa-enrollment` merely to clean up that repository: it is intentionally retained unfinished work.

## Cleanup rule

Before deleting any OceanMail branch in a future cleanup:

1. preserve every branch listed in **Retain — do not delete** unless this file is deliberately updated by a later audited disposition;
2. verify any newly created branch or open PR that did not exist at the 2026-09-11 audit baseline;
3. do not infer preservation from ancestry alone when squash/rebase merge may have changed commit identity;
4. when in doubt, compare the final branch content against the landed merge/squash result or preserve the branch until reconciled.

Git remains the authoritative project record. Chat history is not required to interpret this retention boundary.
