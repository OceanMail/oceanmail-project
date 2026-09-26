# OceanMail Project

This repository is the organization-level documentation and project-memory spine for the OceanMail GitHub organization.

**Git is durable project memory. Chat history is disposable working memory.**

This repository owns current cross-repository OceanMail definition, architecture, terminology, major decisions, repository inventory, workstream orientation, and contributor/AI operating rules. Component repositories remain authoritative for their own source code and implementation-specific documentation.

## Start here

Read, in order:

1. [`PROJECT.md`](PROJECT.md) — concise definition and stable boundaries.
2. [`CURRENT_STATE.md`](CURRENT_STATE.md) — current implementation and work state.
3. [`DECISIONS.md`](DECISIONS.md) — lightweight decision ledger.
4. [`REPOSITORIES.md`](REPOSITORIES.md) — authoritative repository inventory.
5. [`AGENTS.md`](AGENTS.md) — organization-wide contributor/AI instructions.
6. the relevant file under [`workstreams/`](workstreams/).
7. relevant ADRs/specifications/interfaces here and implementation documentation in the owning component repository.

## Authority boundary

`OceanMail/oceanmail-project` owns organization-level truth. It does not duplicate detailed component implementation documentation.

Current implementation repositories:

- [`OceanMail/oceanmail-desktop`](https://github.com/OceanMail/oceanmail-desktop)
- [`OceanMail/oceanmail-station`](https://github.com/OceanMail/oceanmail-station)
- [`OceanMail/oceanmail-server`](https://github.com/OceanMail/oceanmail-server)
- [`OceanMail/oceanmail-infrastructure`](https://github.com/OceanMail/oceanmail-infrastructure)

The five public repositories are cataloged in [`REPOSITORIES.md`](REPOSITORIES.md).

## Documentation rule

Present truth lives in current-state documents. Rationale and supersession live in decision/history documents. Temporary active context lives in scoped handoffs. No important architectural decision may exist only in a handoff, issue, PR, or chat thread.

## Quality baseline

See the [CI quality retrofit specification and tracker](docs/specifications/ci-quality-retrofit.md). G0 is governance only. Diagnostic counts remain unknown until measured; Project application tests/types/coverage are N/A while it is documentation-only. Claude independently reviews every retrofit PR; the owner retains merge and protection authority.


## Contribution and release status

OceanMail 0.2 is experimental, not production-ready or certified distress equipment. Contributors can fork and submit pull requests. See [CONTRIBUTING.md](CONTRIBUTING.md), [SECURITY.md](SECURITY.md), and [publication decisions](docs/specifications/publication-decisions.md). Source and documentation licenses are installed; see [LICENSING.md](LICENSING.md). This repository contains documentation; component build/test instructions belong in their respective repositories. Validate changed relative links and JSON before submitting a documentation PR.


## Source publication and licenses

See [PUBLICATION.md](PUBLICATION.md) for the fresh-history boundary and historical evidence limitations. OceanMail-owned code uses **AGPL-3.0-only**; documentation uses **CC-BY-SA-4.0**. See [LICENSING.md](LICENSING.md), [LICENSE](LICENSE), and [LICENSE-DOCS](LICENSE-DOCS). Third-party terms remain unchanged.
