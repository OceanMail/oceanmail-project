# Privacy cleanup evidence — 2026-09-26 UTC

> Publication scope update — 2026-09-26: the owner approved fresh public repositories for **all five active components: Project, Station, Desktop, Server and Infrastructure**. Preserve the original repositories privately with `-archive` suffixes. The five older BEMPIC/0.1 repositories remain private and frozen. Earlier three-repository scope statements below are superseded historical records.


> Current publication decision (2026-09-26): create fresh sanitized Project, Station and Desktop repositories with installed licenses. Preserve the original repositories privately under names ending in `-archive`. See `PUBLICATION.md` at the repository root. Earlier in-place conversion instructions and pending-license statements below are historical.


Publication scope: **Project → Station → Desktop only**. Server and Infrastructure remain private. Document/privacy review covers all ten repositories.

## Current-file screening

All current text files were searched for personal/operational markers, with identified passages inspected. Downloaded contents were checked against Git blob hashes. Document/notice coverage:

| Repository | Documents/notices |
|---|---:|
| Project | 57 |
| Station | 30 |
| Desktop | 60 |
| Server | 5 |
| Infrastructure | 6 |
| BEMPIC | 41 |
| BEMPIC Reference | 21 |
| OceanMail 0.1 prototype | 56 |
| Infrastructure 0.1 prototype | 16 |
| Server 0.1 prototype | 19 |
| Total | 311 |

This is full-text screening with targeted inspection, not a certification of every historical object or GitHub surface. Five retained active-repository history snapshots additionally screened 713 distinct document blobs across 832 reachable commits. Those snapshots predate the latest cleanup; full archived history is not cleared.

## Remediation

Project #54, Desktop #31, Server #9 and Infrastructure #9 merged after hosted checks. Station #64 tracks the remaining current-tree cleanup and hosted acceptance. Project #55 records the narrowed scope.

Known personal/workstation references and field-site details were generalized; private runner inventory was replaced by generic security requirements. Audit workflows stop generating new full-history bundle artifacts once their respective cleanup PRs merge. Old workflow revisions and existing artifacts remain separate risks.

Sixty issue/PR bodies/comments in the publication candidates were generalized after checking for concurrent edits. Fifty-nine were read back exactly; master #42 was deliberately updated again for scope/decisions. Seventy review summaries across 128 PRs were screened without known-marker findings. This does not remove edited-comment history or historical diffs.

Private recovery snapshots and archive cleanup proposals are retained outside GitHub. No archived repository was modified/unarchived and no visibility change occurred in this pass.

## Remaining blockers

- First-party Git author/committer identities and historical content require a fresh, validated history rewrite using authenticated Git access. Preserve parent/merge topology, unmerged work and third-party attribution. Existing old clones must not reintroduce removed data.
- GitHub-managed PR refs, historical diffs, cached views, edited-comment histories, attachments, old CI logs/artifacts and uninspected surfaces require separate disposition. The available connector cannot perform the necessary history push or artifact/settings/archive operations.
- Archived files include additional personal paths and family/vessel examples. Privacy-only proposals are not applied or tested as executable changes.
- Retained audit artifacts confirmed unexpired: Project 10887143134/10887890292; Station 10887641196/10888676035; Desktop 10886514307/10888157685/10887703983. Some contain full Git bundles. This list is not a complete inventory of all workflow evidence.
- Final exact-ref secret/privacy scans, contributor/ownership/provenance clearance, license files and administrative publication gates remain open.

No complete privacy purge, historical clearance, production/RF proof or permission to publish is claimed. Master tracker: [#42](https://github.com/OceanMail/oceanmail-project-archive/issues/42).


## Artifact deletion update

All seven previously identified audit runs were verified to return zero artifacts after owner deletion on 2026-09-26. Other logs/artifacts remain in the private historical repositories and are not part of the fresh publication.
