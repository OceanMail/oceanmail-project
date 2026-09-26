# Public collaboration and publication policy

> Publication scope update — 2026-09-26: the owner approved fresh public repositories for **all five active components: Project, Station, Desktop, Server and Infrastructure**. Preserve the original repositories privately with `-archive` suffixes. The five older BEMPIC/0.1 repositories remain private and frozen. Earlier three-repository scope statements below are superseded historical records.


Status: **ACTIVE owner direction, 2026-09-26**. All five fresh source repositories are public; source publication does not establish production readiness.
Master tracker: [Project #42](https://github.com/OceanMail/oceanmail-project-archive/issues/42).

## Scope and authority

Maintain public contribution access for Project, Station, Desktop, Server and
Infrastructure in their fresh sanitized repositories. Preserve the five original
development repositories privately under `-archive` names. The five older
BEMPIC/0.1 repositories remain private and frozen; preservation is not development
authorization. Server and Infrastructure are documentation bootstraps.

Historical scope: the 2026-09-25 three-repository restriction is superseded by
the 2026-09-26 five-repository decision. Do not convert the private history
repositories in place. See [PUBLICATION.md](../../PUBLICATION.md).

External contributors, including Rafael, normally receive no organization
membership or Write/Maintain/Admin permission. They read, fork, submit PRs,
review and comment. Maintainers control merges and the owner retains final
project direction. Contribution does not confer architectural authority.
Use topic branches and merge commits; retain review and rollback history.

The owner authorized preparation and safe completed-work merges on 2026-09-25.
The owner subsequently approved the code/docs license choices and zero required
approvals, and required removal of personal/runner information. Licenses are installed in the fresh public repositories. Track remaining rights,
contribution and administrative evidence in publication-readiness.md and issue #42;
publication itself does not establish that every gate passed. Unknown evidence is
a blocker, not a pass.

## Public CI boundary

Use standard GitHub-hosted runners for public PR validation. Before conversion,
remove the repository from every trusted self-hosted runner group's access and
verify public-repository access is disabled. Audit repository-scoped runners too.
Local workstations are never public PR execution targets.

Workflow conditions are defense in depth: a PR can modify its workflow. A
same-repository or private-repository condition does not replace the external
runner access boundary. Public repository workflows must not select trusted
self-hosted runners, including manual, push and scheduled jobs.

Use pull_request, read-only contents permission, pinned Action commits and
checkout persist-credentials: false. Do not use pull_request_target to execute
PR code. Do not pass repository/environment secrets or write tokens into PR
validation. Do not promote untrusted artifacts/caches into privileged release
jobs. Hardware testing is a separate, deliberate maintainer operation against
reviewed exact commits, outside public PR dispatch.

Before publication verify Actions default permissions, external-contributor
approval settings, reusable workflows, apps, keys and collaborator access.
Prepare required checks and main protection before changing visibility; verify
protection immediately afterward. Use an actual non-write external fork to
verify the boundary before converting the next repository. Private-repository
fork restrictions can prevent that exact test before the first conversion;
record that limitation, retain the pre-publication static/settings checks, and
do not describe a same-repository PR as external-fork evidence.

## Privacy and provenance

Audit all refs/history and GitHub surfaces, not just main. Use a maintained
full-history secret scanner and manual review for personal/operational data,
archives, images, fixtures and metadata. Retain scanner version, configuration,
ref inventory, source SHA, report checksum, findings and remediation evidence.
Keep sensitive raw reports private; publish only sanitized conclusions.
Revoke/rotate exposed credentials before any publication. Current-tree deletion
does not remove historical exposure. History rewriting requires a deliberate
owner disposition and coordination with retained PR refs, caches and clones.

Preserve upstream copyright, license, exact source revision and modification
notices. Record copied/adapted/generated inputs and asset provenance. AI-assisted
work remains subject to the same review and attribution requirements; generated
text is not evidence of rights clearance. Never certify another person's DCO
sign-off or claim ownership on their behalf.

## Defensive publication

OceanMail does not pursue patents by default for licensing revenue or exclusion.
Preserve freedom to use OceanMail-developed technology through open, technically
meaningful publication. Disclosures should identify the problem, mechanism,
protocol/state semantics, implementation or pseudocode, failure conditions,
version/date and prior art. Separate implemented evidence from design proposals.

Initial disclosure index: ADR-007 capacity tiers; ADR-008 lease/fairness/channel
semantics; ADR-009 personal-traffic boundaries; delivery-evidence-and-repair.md;
and the upstream-provenance/prior-art registers. These are disclosure candidates,
not assertions of novelty or patentability.

At an approved publication baseline, record exact commits, a tag/release date,
source archive checksum and durable public URL. External archival may follow
for significant disclosures; it is not required for the first repository.
A private Git timestamp alone does not establish public accessibility. Preserve
public availability evidence. If a later patent concern arises, retain the
dated disclosure and claim comparison for qualified review; do not assert
automatic invalidity. Publication does not resolve earlier third-party rights.

## Remaining owner decisions

Code/docs license choices are approved; inbound contribution terms and ownership attestations remain pending in
[publication-decisions.md](publication-decisions.md). Security-reporting activation,
administrative access verification and historical privacy disposition also remain
publication gates. None is silently adopted by this document.

Source publication is separate from binary redistribution, service operation,
radio authorization and production readiness. Encryption/export publication
obligations must be evaluated for the material actually shipped. Emergency
features are experimental and do not replace certified distress equipment.

