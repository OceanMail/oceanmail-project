# OceanMail Publication Readiness

Status: **ACTIVE release/publication gate**

This specification defines the minimum review required before any currently private OceanMail repository is made public or used as the source for a public source release. It does **not** select a license or certify a repository for publication. The owner's 2026-09-25 preparation scope and contribution model are recorded in [public-collaboration.md](public-collaboration.md); historical snapshots below do not override that newer direction.

## Separate decisions

Treat these as separate decisions:

1. making a Git repository/history public;
2. releasing OceanMail source under an explicit license;
3. distributing built binaries/installers/appliances;
4. operating a hosted OceanMail service;
5. publishing generic deployment examples versus production operations material.

Passing one boundary does not imply approval for the others.

## Visibility-change rule

Do not change a private repository to public visibility merely because its current `main` tree looks safe.

Before a visibility change, obtain explicit owner approval after the gates below are reviewed. If historical material is unsuitable for publication, prefer a reviewed/sanitized public history or new public repository over exposing the existing private history by default.

## Required audit gates

### 1. Current-tree content

Review the complete current tree for:

- credentials, tokens, private keys, passwords, certificates, API secrets, signing material, or recoverable secret values;
- production/customer data or private mailbox/message content;
- internal hostnames, addresses, topology, operational endpoints, or deployment detail that should remain private;
- real-world field-test locations, personal contacts/tester identities, vessel/site details, or other unnecessary personal/operational information;
- screenshots, logs, fixtures, evidence bundles, generated files, or archives that contain any of the above;
- private operational instructions that belong in Infrastructure or another private operational record rather than public product source.

A normal source-code security design, API contract, or threat model is not automatically sensitive merely because it describes security behavior. The concern is live/private operational material, secrets, personal information, and data that creates avoidable exposure.

### 2. Full Git and GitHub history

Audit more than the checked-out branch. Publication of an existing repository can expose historical material that was deleted from `main`.

Review, as applicable:

- all reachable commits, branches, tags, and historical blobs;
- commit author/committer metadata that may expose personal contact information;
- pull-request and issue bodies, comments, reviews, and attachments;
- historical test evidence, local paths, machine names, real site descriptions, and copied diagnostic output;
- GitHub Actions artifacts/logs and other retained repository-adjacent evidence where publication would expose them.

Run a full-history secret scanner before approval. Current-tree greps alone are insufficient.

### 3. Project and third-party licensing

Each public source repository needs an explicit project license or an explicit documented reason that it is source-visible but not licensed for reuse. Do not assume public GitHub visibility grants reuse rights.

Before publication:

- add/review the repository's top-level `LICENSE` and copyright notices;
- identify bundled, copied, patched, generated-from, or redistributed third-party material;
- preserve required upstream licenses/notices and patch provenance;
- confirm license compatibility for the form in which components are combined or distributed;
- keep HERMES/Mercury and other lower-layer upstream code separate where the accepted upstream-first boundary requires it.

Repository visibility and binary redistribution can have different obligations. Re-check licenses at the actual distribution boundary.

### 4. Desktop / Thunderbird redistribution boundary

For `OceanMail/oceanmail-desktop`, source publication of OceanMail-owned code is distinct from distributing an OceanMail-branded Thunderbird-derived application package.

Before public binary distribution, resolve and document the existing Decision 0005 gates for:

- Thunderbird/Mozilla source-license compliance;
- redistribution of the pinned Thunderbird base;
- branding/trademark use and removal/replacement where required;
- update/source-availability obligations;
- any downstream Thunderbird patches, if later introduced;
- coexistence and uninstall behavior for the packaged product.

Do not infer that making the OceanMail repository public completes these distribution obligations.

### 5. Station / HERMES-Mercury provenance boundary

For `OceanMail/oceanmail-station`, preserve the current upstream-first separation and the exact provenance of any required downstream laboratory/integration patch.

Before publication/release:

- re-check the exact licenses of pinned HERMES/Mercury/libcmime dependencies used by the distributed form;
- preserve upstream notices and patch provenance;
- do not silently relicense third-party GPL/AGPL material as OceanMail-owned code;
- audit Station field-test/research documents for real sites, personal contacts, vessel/site capabilities, and workstation-specific material that has no need to be public.

The tracked HERMES laboratory patch and provenance notice are implementation evidence, not a license choice for OceanMail Station itself.

### 6. Security and default-exposure review

Public source is not itself a reason to hide security architecture. The release gate is that publication must not expose live secrets or accidentally publish an unsafe operational configuration as production-ready.

For each component verify:

- development credentials/fixtures are unmistakably non-production;
- insecure laboratory modes are clearly gated and cannot be mistaken for production readiness;
- default network exposure matches the documented security boundary;
- public CI is safe for contributions/forks, especially where self-hosted runners are used;
- security reporting instructions exist before inviting outside contributors/users.

### 7. Public-repository hygiene

Before opening a repository to outside contributors, decide and add as appropriate:

- `LICENSE`;
- `SECURITY.md`;
- `CONTRIBUTING.md`;
- third-party notices/attribution;
- trademark/branding statement where relevant;
- issue/PR templates and contribution expectations;
- supported/release status so experimental 0.2 code is not mistaken for production service.

## Current 0.2 audit snapshot — 2026-09-11

This is a readiness snapshot, not a publication decision.

### `OceanMail/oceanmail-desktop`

- Private.
- Technically plausible public-source candidate.
- No top-level `LICENSE` is currently present.
- Decision 0005 already requires explicit Thunderbird redistribution/update/trademark/source-compliance work before public distribution.
- A full-history/GitHub-surface review and secret scan remain required before any visibility change.

### `OceanMail/oceanmail-station`

- Private.
- Technically plausible public-source candidate, but **not ready for a blind visibility flip**.
- No top-level `LICENSE` is currently present.
- Upstream license/provenance handling is materially documented, including the tracked HERMES laboratory patch.
- `docs/testing-hardware-acquisition-plan.md` contains real-world field-test geography, personal-contact categories, vessel/site capabilities, and local development-resource detail; it must be sanitized, generalized, relocated to a private record, or intentionally approved before public publication.
- Historical PRs/commits/evidence may contain workstation-specific paths, machine names, exact laboratory IDs, and older site/test details; audit full history rather than only current `main`.

### `OceanMail/oceanmail-server`

- Private and bootstrap-level.
- No top-level `LICENSE` is currently present.
- Current contents are mostly boundary/documentation, but the long-term public/private source model for hosted service implementation is not settled.
- Do not infer a business/service-source decision from Desktop or Station publication choices.

### `OceanMail/oceanmail-infrastructure`

- Private and explicitly described by its repository README as the private deployment/operations repository.
- No top-level `LICENSE` is currently present.
- Its ownership boundary includes topology, DNS/TLS/networking, monitoring, backup/recovery, gateway/VPS operations, and secret-management boundaries; this is the repository most likely to accumulate material that should not be exposed wholesale.
- If public reproducible deployment examples are later desired, consider a separate generic/sanitized deployment/examples repository rather than making production operations history public by default.

## Approval outcome

A publication review should end with an explicit per-repository disposition, for example:

- `PUBLIC — approved existing history`;
- `PUBLIC — publish sanitized/new history`;
- `PRIVATE — operational/business/security boundary`;
- `DEFERRED — unresolved licensing/product strategy`.

Record the final disposition in the project decision ledger or an ADR if it materially changes repository/product architecture.

