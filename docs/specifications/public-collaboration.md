# Public collaboration policy

Status: **ACTIVE — updated 2026-09-26**.

## Scope and authority

Project, Station, Desktop, Server and Infrastructure are public source repositories.
Server and Infrastructure are bootstraps. See [PUBLICATION.md](../../PUBLICATION.md).

External contributors read, fork, submit PRs, review and comment without organization
membership or upstream Write/Maintain/Admin permission. Maintainers control merges;
the owner retains final project direction. Use topic branches and merge commits.
The installed licenses apply; no DCO or additional inbound agreement is adopted.
See [publication decisions](publication-decisions.md).

## Public CI boundary

Use standard GitHub-hosted runners for public PR validation. Keep the repository excluded from every trusted self-hosted runner group's access and
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

Maintain read-only Actions defaults, contributor-approval settings, protected main,
required checks, and reviewed app/key/collaborator access. An end-to-end test with
an external fork and a non-write contributor remains unverified. Record that test
separately from same-repository PR validation.

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

The license and contribution decisions are recorded in
[publication-decisions.md](publication-decisions.md). Additional contribution
agreements have not been adopted.

Source publication is separate from binary redistribution, service operation,
radio authorization and production readiness. Evaluate obligations for the material
actually shipped. Emergency features do not replace certified distress equipment.
