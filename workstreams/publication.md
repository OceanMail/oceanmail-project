# Publication / Open-Source Readiness Workstream

> Publication scope update — 2026-09-26: the owner approved fresh public repositories for **all five active components: Project, Station, Desktop, Server and Infrastructure**. Preserve the original repositories privately with `-archive` suffixes. The five older BEMPIC/0.1 repositories remain private and frozen. Earlier three-repository scope statements below are superseded historical records.


## Current priority

Maintain public fork/PR access for all five active components: **Project, Station,
Desktop, Server and Infrastructure**. All five fresh sanitized source repositories
are public with installed licenses. Their original development repositories remain
private under `-archive` names; the five older BEMPIC/0.1 repositories remain
private and frozen. Server and Infrastructure are documentation bootstraps.

Track cross-repository follow-up in [#42](https://github.com/OceanMail/oceanmail-project-archive/issues/42)
and [PUBLICATION.md](../PUBLICATION.md). Contribution access does not confer
upstream write permission. Public source does not establish production readiness,
binary redistribution approval or radio authorization.

## Historical preparation record — superseded

The sections below record pre-publication gates and observations from 2026-09-25.
They are retained as history, not current scope or current completion claims.
The three-repository restriction and proposed in-place conversions are superseded.

### Required gates at that time

Follow [publication-readiness.md](../docs/specifications/publication-readiness.md) and [public-collaboration.md](../docs/specifications/public-collaboration.md). Code/docs license choices and zero required approvals are approved; contribution/rights and license installation remain pending, as recorded in [publication-decisions.md](../docs/specifications/publication-decisions.md). No repository has passed publication review yet.

Project is tracked in [#48](https://github.com/OceanMail/oceanmail-project-archive/issues/48). Its initial current tree is documentation-only, with no license or workflows. Current-tree privacy cleanup does not clear full-history or GitHub-surface exposure. Station/Desktop hosted workflow migrations are merged; externally enforced trusted-runner exclusion remains unverified. Server and Infrastructure are bootstrap documentation repositories.

### Blocked decisions and access at that time

- Contributor terms and rights to existing material; approved license files still need installation after provenance clearance.
- Apply the owner-required removal of historical personal/operational data, including Git identities, PR refs and retained copies.
- Final exact-ref rescan and privacy/provenance disposition. Initial authenticated history scans are recorded in [the audit evidence](../docs/publication/2026-09-25-audit.md); shell clone access was worked around using private hosted audit bundles.
- Administrative evidence for runner groups, collaborators/apps/keys, Actions defaults, private vulnerability reporting and main protection. The current connector returns 403 on protection reads.
- External non-write fork acceptance after the first conversion and before the next.

No-patent/default defensive-publication direction is settled. Public source does not mean production readiness, binary redistribution approval or radio authorization. Server and Infrastructure remain private under the latest owner direction; no conversion of either is planned.

### Completed preparation at that time

Project #49/#50/#51, Station #60, Desktop #27/#28 and Server/Infrastructure #7 are merged. Project hosted documentation checks and Desktop source/synthetic-merge lint plus 100 tests pass. Full-history scans now cover all five active repositories; the audit record distinguishes zero findings from Station's verified checksum/example-token false positives. No repository visibility or administrative protections were changed.

Administrative cutover remains blocked; use the [settings handoff](../docs/publication/admin-cutover.md) after owner decisions and final privacy/provenance clearance. Station #63 is the isolated libcmime patch/notice remediation, with integration evidence tracked in that PR.

Station #61/#63 and Desktop #30 are also merged: staged component guidance, explicit libcmime provenance/notices and the development-tool dependency fix. See the audit record for exact heads and test evidence. Station scanner false positives are explicitly dispositioned while preserving the raw failure; all repositories remain private pending owner/admin gates.
