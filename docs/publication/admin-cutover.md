# Administrator cutover checklist

> Current publication decision (2026-09-26): create fresh sanitized Project, Station and Desktop repositories with installed licenses. Preserve the original repositories privately under names ending in `-archive`. See `PUBLICATION.md` at the repository root. Earlier in-place conversion instructions and pending-license statements below are historical.


Status: preparation only, 2026-09-25. Master [#42](https://github.com/OceanMail/oceanmail-project-archive/issues/42).
This is the reviewable settings handoff for Project first; it does not authorize
visibility while any gate is unresolved. The available GitHub connection returns
403 on branch-protection reads and cannot verify the administrative surfaces below.

## Before changing visibility

1. Resolve [owner decisions](../specifications/publication-decisions.md), including
   rights to existing material and historical personal/operational metadata. Apply
   approved licenses/contribution terms and complete the final exact-ref audit.
2. Record organization base permission and repository collaborators/teams. External
   contributors need no membership or write permission. Review maintainers, admins,
   installed apps, deploy keys and token scopes; retain only required access.
3. Inspect every organization runner group and repository-scoped runner. Exclude
   the repository from all trusted runners, including all restricted groups.
   Disable public-repository access on trusted groups. A workflow condition or
   requirement to approve a run does not prevent a PR from selecting another runner.
4. Set default Actions tokens read-only; disable Actions creation/approval of PRs
   unless explicitly needed. Keep write tokens and secrets disabled for fork PRs.
   Require approval for all outside contributors as an additional control. Confirm
   environment, reusable-workflow, cache/artifact and app paths cannot bypass this.
5. Enable private vulnerability reporting and verify a non-maintainer can find the
   private report route. Update SECURITY.md from pending to verified only afterward.
6. Review issues, reviews, releases/assets, logs/artifacts, packages, wiki/discussions,
   environments/deployments and Pages. Private audit artifacts include full Git
   bundles: remove/expire them before visibility unless every contained ref and
   metadata value is cleared. Preserve necessary restricted evidence elsewhere.
7. Prepare [Project main protection](main-protection.proposed.json). Resolve its
   approval count before application: zero for a sole maintainer, or one when an
   independent human reviewer is available. Keep PRs, current-branch checks, resolved
   conversations, admin enforcement, force-push/deletion blocks and merge commits.
   Do not require linear history. Configure the observed check `docs`.
8. Verify administrative access can apply and read back protection at cutover. If
   the current plan permits private protection, apply and test it first. Otherwise
   have the exact accepted payload and working administrator session ready; do not
   change visibility with only this restricted connection available.

## One repository at a time

After every pre-publication gate passes, change Project visibility and immediately
apply/read back protection. Verify anonymous access, intended license/docs/history,
private reporting, security/dependency/secret-scanning settings and CI. Record the
actual accepted settings, exact published SHA and timestamp in its readiness issue.

Use a real non-write account/fork for a harmless PR. Verify upstream push and merge
are denied, commenting/review work, CI runs on GitHub-hosted runners with no useful
write token/secrets, and the maintainer can merge using a merge commit. Do not run
untrusted code on a trusted runner as a test. If a check fails, stop conversion of
the next repository and remediate. Rafael need not receive write access for this.

## Observed main workflow inventory

The initial 11 workflows on the five active main branches were inspected on 2026-09-25.
With Station #61 merged there are 12 workflows, all selecting Ubuntu 24.04 on GitHub-hosted runners and contents:read. No current main
workflow uses pull_request_target, issue_comment, workflow_run, schedule, shared
cache restoration or secret interpolation. Historical branches still contain old
runner configurations; the administrative exclusion remains essential.

| Repository | PR checks | Other workflows/events |
|---|---|---|
| Project | docs; every PR/push | Private audit: named audit branch push/manual |
| Station | phase3a, phase4i, auth; every main PR | Same checks on main/CI migration branch push/manual; private audit on named branch push/manual |
| Server | docs; every PR/push | Private audit: named audit branch push/manual |
| Desktop | lint; every PR/push | Private audit: named audit branch push/manual |
| Infrastructure | docs; every PR/push | Private audit: named audit branch push/manual |

Public checks disable checkout credential persistence. Private audit workflows are
private-repository-gated, retain a read-only credential only to fetch all refs, and
remove it before scanning; they execute no application code. Their scanner is
checksum-pinned and ignores repository suppression/configuration files. Raw scan
results and manual false-positive triage are distinct evidence, not privacy or
license clearance. Station's additional private audit merged in PR #61 after hosted acceptance and
explicit manual disposition of the unchanged checksum/example-token findings.
Its raw scanner exit remains nonzero; it is not a required public PR check.

