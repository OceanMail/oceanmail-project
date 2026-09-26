# CI quality retrofit rollout

Status: G0 and Station S1 merged by owner; Station S2 authorized in #56 and in draft review. S3a remains unassigned.
Prepared 2026-09-22 from the owner-supplied OceanMail CI retrofit kit.
Updated 2026-09-23 for owner-merged G0/S1 and assigned Station S2.
Tracking: [Project #43](https://github.com/OceanMail/oceanmail-project-archive/issues/43),
[Station #53](https://github.com/OceanMail/oceanmail-station-archive/issues/53),
[Station #56](https://github.com/OceanMail/oceanmail-station-archive/issues/56).

## Scope and authority

Codex implements, ChatGPT plans/triages, Claude independently reviews **every**
retrofit PR against its exact base/head, and the owner decides merge/protection.
A draft PR or green check does not authorize merge or another phase.
Station precedes Desktop, followed by documentation-only Server, Infrastructure
and Project gates. G0 is the coordination prerequisite, not Project lint rollout.
No component implementation internals are copied here. Archives stay untouched.

## Baseline and evidence policy

Measure before changing code. Retain raw commands, working directories, exit
statuses, timeouts, tool/config/lock provenance, source SHA and dirty state.
Missing tools, parser/setup/collection failures, partial scans, absent coverage
and zero tests are explicit gaps, never zero findings or passing acceptance.
Report-only exit zero means report generation, not clean CI.

Later seed tasks freeze diagnostic identities and multiplicity with source
context, reason, owner and tracking issue; advisory exceptions also expire.
Reject additions, equal-count replacements, widened suppressions and changed
suppressed statements without review. Shrink debt; never baseline compiler
errors or hide broken setup. Keep the unsuppressed report. Changed executable
lines will require 80% coverage with unexecuted owned source retained. These
are future adapter/gate requirements, not enforcement claimed by G0 or S1.

Separate STATIC / UNIT, INTEGRATION and LIVE / PRODUCT evidence. Record exact
branch-head and synthetic-merge SHAs/event types separately; no stale green run
may support a newer head. Post-merge main evidence requires owner merge first.
Preserve Station Phase 4I receipt trust `lab_peer_transport_unverified`, exact
upstream pins and failed/retried evidence. Queue disappearance is not delivery.
No physical-radio Phase 5 is authorized by CI retrofit phase numbers.

Tooling, mechanical cleanup, adapters, seed and workflow PRs stay separate.
Characterization tests lock current behavior without asserting correctness.
Audit bugs require a reproducing failing test on unchanged code; hypotheses
remain separate. ChatGPT triages, owner approves, then one fix/regression PR per
approved bug proves red-to-green. No application changes in measurement tasks.

## Verified inventory and count tracker

Live GitHub repository metadata, default-branch commits and recursive trees are
captured in [inventory-2026-09-22.json](../quality/inventory-2026-09-22.json).
Five active, five archived; archive administration was not changed. The SHA is
an inventory snapshot, not a test result. All unmeasured lint/type/Semgrep/advisory and test
exception counts remain **unknown**. Station S1 measurements are linked below;
the other repositories have inventory-only evidence. Docs-only application type/test/coverage metrics are **N/A**; tooling
metrics still need measurement. No repository is declared retrofit-complete.

| Repository | Inventory / measured SHA | State | Phase / owner | Lint / types / security / test exceptions | Coverage by module | Next / evidence / last measurement |
| --- | --- | --- | --- | --- | --- | --- |
| `bempic` | `819bfd34e14822960afb969fc14980293a59bac5` | Archived | Excluded / owner | Historical; unmeasured | Historical; unmeasured | No changes / inventory only / none |
| `bempic-reference` | `c182f1dd42d64e3117e505904ce06696057ee9c3` | Archived | Excluded / owner | Historical; unmeasured | Historical; unmeasured | No changes / inventory only / none |
| `oceanmail-0.1-prototype` | `5761fdf5a823e5ae7ccb1d81846a19156b87ed73` | Archived | Excluded / owner | Historical; unmeasured | Historical; unmeasured | No changes / inventory only / none |
| `oceanmail-infrastructure-0.1-prototype` | `5daf16ae0501df603d11bf29cdf0b748e72ec22b` | Archived | Excluded / owner | Historical; unmeasured | Historical; unmeasured | No changes / inventory only / none |
| `oceanmail-server-0.1-prototype` | `3d2bebc47e6c918fc7270e2fcec392b10b7d5542` | Archived | Excluded / owner | Historical; unmeasured | Historical; unmeasured | No changes / inventory only / none |
| `oceanmail-desktop` | `4931be00f3df1398c53d032b21863985918fb75f` | Active | Not started / Codex | Unknown | Unknown | See task register / inventory only / none |
| `oceanmail-server` | `9a21d2493ceb5eb6b760aebd42a81493218850ce` | Active | Not started / Codex | Unknown; application types/tests N/A | Application N/A | See task register / inventory only / none |
| `oceanmail-infrastructure` | `228b6d3602d39843eefce1c3aba454e1a6c0f90b` | Active | Not started / Codex | Unknown; application types/tests N/A | Application N/A | See task register / inventory only / none |
| `oceanmail-station` | `f9c4fc6ca392d99f110fa18e892c70f5f757da11` (S1 PR head) | Active | S1 merged; S2 draft / Codex; Claude review pending | Clippy 4 emissions; ShellCheck 23 unsuppressed; Ruff 0; Python strict types 296; Semgrep 1 INFO; product advisories 0; tools: see report; observed test skips/xfail 0 | [Seven-file report](https://github.com/OceanMail/oceanmail-station-archive/blob/f9c4fc6ca392d99f110fa18e892c70f5f757da11/docs/quality/S1-MEASUREMENT.md#rust-file-coverage) | [Merged #54](https://github.com/OceanMail/oceanmail-station-archive/pull/54) / S1 measured 2026-09-22; [S2 evidence](../quality/station-s2-2026-09-23.md) / 2026-09-23 |
| `oceanmail-project` | `7b911b57491b7c3aa6dc599f9003c1e69dafb741` | Active | G0 merged; S2 tracking draft / Codex | Unknown; application types/tests N/A | Application N/A | See task register / inventory only / none |

Station source/tooling measurement was sealed at
`2f22edba9a57ae7782fec0f9f27b81f555eaaed5`; subsequent commits add only the
measurement document/raw archive and correct a Clippy target label. A clean final-head rerun reproduces the same
test outcomes, diagnostic totals and per-file coverage. See the
[component report and raw archive](https://github.com/OceanMail/oceanmail-station-archive/blob/f9c4fc6ca392d99f110fa18e892c70f5f757da11/docs/quality/S1-MEASUREMENT.md).
The strict Python total includes 67 existing helper diagnostics and 229 new
measurement-tool diagnostics under the provisional strict configuration; no
baseline acceptance is implied. Hadolint remains partial on one Dockerfile.
No product or test-source change was made to improve measurements.

Existing no-radio `workflow_dispatch` runs on that exact final Station head:
[Phase 3](https://github.com/OceanMail/oceanmail-station-archive/actions/runs/35790761626),
[Phase 4I](https://github.com/OceanMail/oceanmail-station-archive/actions/runs/35790764446),
[Phase 4J](https://github.com/OceanMail/oceanmail-station-archive/actions/runs/35790767763).
All three completed successfully on 2026-09-22 using a private CI environment, with the exact final head above. Phase 4I retains its durable
snapshot, exact far-side mailbox, cleanup, negative pre-return, byte-identical
receipt, correlation and restart assertions; trust remains
`lab_peer_transport_unverified`. Logs and artifacts are retained in the component
PR review handoff. Earlier unstarted dispatches on the superseded documentation
head were cancelled and provide no acceptance evidence. No synthetic-merge run
exists for that path-filtered S1 diff. The owner subsequently merged #54 at
`8aced292c745fb8c81af387f57c1a92246198a74` and authorized S2 in #56.
Actual-main post-merge acceptance was missing and is now recorded separately
as workflow_dispatch in the [S2 evidence](../quality/station-s2-2026-09-23.md);
it is not main-push evidence. S2 draft #57 requires independent Claude review;
S3a remains unauthorized.

## Separate task register

Each listed ID is a separate bounded concern (parameterized fixes/burn-downs
are separate PRs per bug/module). Every row has an accountable owner and status.
Codex-owned tasks also have Claude review and ChatGPT triage; human operations
remain the owner's work. G0 and S1 are merged; S2 is currently assigned. Future issue/PR
links are pending rather than fabricated.

| Task / repository | Concern | Owner | Status / next evidence |
| --- | --- | --- | --- |
| G0 / Project | Governance, inventory, phase register | Codex | Merged #44 at `0a55c1ee5b77d6637c4b181150c17819bab572e0`; #43 |
| S1 `quality/measure` / Station | Phase 1 report-only tooling and scope: pin compatible tools, identify feature/target/test matrix; collect Rust, shell, Python, lab/static, Semgrep and dependency measurements; update local agent commands. | Codex | Merged #54 at `8aced292c745fb8c81af387f57c1a92246198a74`; original measurements retained; actual-main acceptance recorded with S2 |
| S2 `quality/mechanical` / Station | Phase 2, title `Mechanical cleanup — no logic changes`. cargo fmt plus reviewed safe Python/shell formatting where applicable. No cargo clippy --fix by default. | Codex | Authorized #56; draft #57; [before/after and CI evidence](../quality/station-s2-2026-09-23.md); Claude review pending |
| S3a `quality/ratchet-adapters` / Station | Tooling only: implement/test Clippy, shellcheck, Python type, audit and config/suppression adapters described in CI-CONTRACT.md. No production cleanup or baseline seeding. | Codex | Not started; requires separate assignment |
| S3b `quality/baseline` / Station | Freeze measured residual diagnostics; exact targeted expected failures/issues if any; README ledger and type/lint policies. | Codex | Not started; requires separate assignment |
| S4 `quality/ci` / Station | Instantiate ci-rust-station.yml plus shell/Python fragment and actual locked configs. Integrate existing auth/readiness tests. Preserve Phase 3 and Phase 4I jobs; remove no evidence checks. | Codex | Not started; requires separate assignment |
| S5 human / Station | Branch protection and runner boundary verification, not an agent PR. | Owner | Not started; requires separate assignment |
| S6a `test/characterize-auth` / Station | Tests only for uncovered auth.rs cases: principal/account isolation, malformed credentials, revoked/invalid grants, persistence failures as applicable to current code. | Codex | Not started; requires separate assignment |
| S6b `test/characterize-state-evidence` / Station | Tests only, one uncovered unit per PR within src/lib.rs or receipt/evidence binaries: persistence/restart/dedup/correlation/input parsing. | Codex | Not started; requires separate assignment |
| S6c `test/characterize-lease` / Station | Tests only for uncovered src/lease.rs boundaries: timing/expiry/preemption/state transitions within implemented policy. | Codex | Not started; requires separate assignment |
| S7 per-module audit / Station | Claude writes reproducing tests on audit branches; ChatGPT triages; owner approves. | Claude | Not started; requires separate assignment |
| S7-fix-ISSUE / Station | One approved fix and its regression test per PR, labeled bug fix. | Codex | Not started; requires separate assignment |
| S8 `quality/burndown-MODULE` / Station | One module's accepted diagnostic/type debt, with focused tests if behavior changes. | Codex | Not started; requires separate assignment |
| D1 `quality/measure` / Desktop | Report-only ESLint/Prettier/checkJs, existing custom lint/node tests, complete extension/script coverage, Semgrep and npm audit. | Codex | Not started; requires separate assignment |
| D2 `quality/mechanical` / Desktop | Safe ESLint fixes plus Prettier; title `Mechanical cleanup — no logic changes`. | Codex | Not started; requires separate assignment |
| D3a `quality/ratchet-adapters` / Desktop | ESLint/type/audit/config and coverage-path adapters with tooling tests. | Codex | Not started; requires separate assignment |
| D3b `quality/baseline` / Desktop | Seed exact legacy diagnostics and any strictly justified known failing tests; document ledger/issues/source scope. | Codex | Not started; requires separate assignment |
| D4 `quality/ci` / Desktop | Instantiate JavaScript template plus shell checks; keep existing custom lint and node tests. Retain current workflow until equivalent coverage is verified. | Codex | Not started; requires separate assignment |
| D5 human / Desktop | Owner enables branch protection. | Owner | Not started; requires separate assignment |
| D6a `test/characterize-station-auth` / Desktop | Tests only for uncovered station/lab-auth-client.js and station-client.js behavior, one module per PR. | Codex | Not started; requires separate assignment |
| D6b `test/characterize-available` / Desktop | Tests only for uncovered Available planner/model edges, one module per PR. | Codex | Not started; requires separate assignment |
| D6c `test/characterize-evidence-lifecycle` / Desktop | Tests only, one module per PR: sent-status model or Experiment cleanup/profile coexistence. | Codex | Not started; requires separate assignment |
| D7 / fixes / D8 / Desktop | Same independent audit, one-bug-per-PR fix, and one-module debt burn-down contract as Station. | Codex | Not started; requires separate assignment |
| V1 `quality/measure-docs` / Server | Inventory three Markdown files; report-only Markdown/link checks; add quality commands to AGENTS/CLAUDE. | Codex | Not started; requires separate assignment |
| V2 `quality/mechanical-docs` / Server | Mechanical Markdown formatting only, if violations warrant a PR. | Codex | Not started; requires separate assignment |
| V3 `quality/docs-baseline` / Server | Implement/test documentation adapters, seed exact style/link exceptions and ledger; document tooling dependencies. | Codex | Not started; requires separate assignment |
| V4 `quality/ci-docs` / Server | Instantiate documentation workflow. | Codex | Not started; requires separate assignment |
| V6 future / Server | At first application module, establish its actual stack's lint/types/tests/security/coverage gate before merging application growth. | Codex | Not started; requires separate assignment |
| I1 `quality/measure-docs` / Infrastructure | Inventory four Markdown runbooks, report-only docs/link checks; record current runner model. | Codex | Not started; requires separate assignment |
| I2 `quality/mechanical-docs` / Infrastructure | Mechanical document formatting only if needed. | Codex | Not started; requires separate assignment |
| I3 `quality/docs-baseline` / Infrastructure | Tested docs adapters/ledger and executable-source introduction guard. | Codex | Not started; requires separate assignment |
| I4 `quality/ci-docs` / Infrastructure | Documentation workflow plus tooling dependency audit. | Codex | Not started; requires separate assignment |
| I6 future / Infrastructure | Before executable deployment code lands: shell/schema/IaC validation and isolated fixtures, then module-level characterization/audit. | Codex | Not started; requires separate assignment |
| P1 `quality/measure-docs` / Project | Report-only Markdown, local links/anchors, decision/index/workstream reference checks. | Codex | Not started; requires separate assignment |
| P2 `quality/mechanical-docs` / Project | Mechanical formatting only if needed. | Codex | Not started; requires separate assignment |
| P3 `quality/docs-baseline` / Project | Tested docs/reference adapters and exact exception seed. | Codex | Not started; requires separate assignment |
| P4 `quality/ci-docs` / Project | Required quality documentation workflow. | Codex | Not started; requires separate assignment |
| P8 `quality/burndown-SECTION` / Project | One documentation section's accepted style/link debt per PR. | Codex | Not started; requires separate assignment |

The combined D7/fixes/D8 shorthand above means three distinct task families:
D7 audits (Claude), D7-fix-ISSUE (Codex) and D8 burndown-MODULE (Codex), all
not started. No combined implementation PR is permitted.

## Review and completion

Claude inspects actual diff, exact base/head, full findings, test identities and
outcomes, scope/exclusions, tool failures, coverage paths and CI logs. Report
severity, reproduction, observed invariant, gaps and recommendation. Each future
gate needs an isolated negative probe; do not infer gate enforcement from a
green report. Owner protection follows required green main CI and verified
runner boundaries; public/fork code never runs on persistent trusted
runners. An active-code repo is complete only after verified required CI,
documented baseline, characterization of identified high-risk gaps, triaged
audit findings and current burn-down evidence. Documentation-only repositories
require a source-introduction guard and mark product characterization N/A.
Archives are excluded/historical, not CI-complete.

## Kit provenance

Owner-supplied kit dated 2026-09-22. SHA-256 below identifies the input documents;
these hashes and kit tests do not prove repository CI acceptance. Component
commands/configuration/reports belong in their owning repositories.

| Input | SHA-256 |
| --- | --- |
| `README.md` | `113f7b224bb8d4d8ad92e98cbc577836b2dc693c47e57f41ab50c684d65d0281` |
| `EXECUTION-PLAN.md` | `f3bc8ba7fad7bdd4d072cfd1d9aadc9f117a37b9d2d3a087d2516ecc942249c9` |
| `CI-CONTRACT.md` | `49427a0eca9653d670ba7e2a6bff7e4d9e49c54ae23f7d517f0397ebfe5230a2` |
| `REVIEW-CHECKLIST.md` | `093984c21a09291378aa6e0df884597f8c60b50ff97d05e564b2fc52f18dd21a` |
| `INVENTORY.md` | `a6e4d2b3e4f4d92a90b8ff6bef2eefe881b984a588f7df8a1f25eb720500c9d3` |

