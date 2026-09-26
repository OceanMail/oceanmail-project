# Station S3a public port — 2026-09-26

[Public Station PR #4](https://github.com/OceanMail/oceanmail-station/pull/4)
contains the implementation port.

The owner assigned review and selective public porting of the remaining archive
work. This is a tooling proposal, not an accepted baseline or CI rollout.

## Sources and preservation

- Station archive PR #59: `a2487dd6640631785438539d7eb4e7e845144ba8`.
- Project archive PR #46: `04dc599c9ab65f7ccf77b701294e01c4399182af`.
- Public Station base: `5d6b95ebc434d85beaedc093a831ab01841f79c3`.
- Public Project base: `e9009f0e764d4b06d048ee9ae1917f42ee90169e`.

The Station archive branch contains older HERMES/Mercury work alongside S3a.
Only the quality tooling, tests/locks, documentation and existing Rust toolchain
selection are ported. The public dependency selections, retirement regression
patch, product source and existing acceptance workflows remain authoritative.
Archive source branches remain until public replacements are accepted.

Project tracking is rewritten around the public proposal. Private historical
log bundles and old head-specific results are not republished as new evidence.
S2 archive Station #57 and Project #45 were merged on 2026-09-25; earlier tracker
language saying S2 remained draft was stale. That historical acceptance does not
accept S3a or authorize S3b/S4.

## Review and evidence

Implementation details and reproduction commands belong in Station's
[public S3a handoff](https://github.com/OceanMail/oceanmail-station/blob/54251d51f6dcc34ea2dce7b8bc7d6a46d9c40a70/.quality/S3A-HANDOFF.md).
The port review found and fixed measurement of multi-option ShellCheck disable
comments, with a regression test. Historical archive counts are not current
public results. Exact final heads, fresh local evidence and hosted workflow
results are recorded in the paired public PRs.

STATIC / UNIT comprises tooling tests, live scanner fixture probes and fresh
report-only measurement. Existing hosted no-radio acceptance is INTEGRATION.
There is no LIVE / PRODUCT, physical-radio or production-security claim.

Independent Claude review of each exact public base/head remains required by
AGENTS.md and the retrofit specification, followed by owner acceptance. A green
workflow does not satisfy that review. No production suppression/advisory ledger,
baseline, required quality workflow or protection setting is introduced.

## Independent review follow-up

Claude independently reviewed Station `8fa010c24beb2b639350991a21ed14406f1c633c`
and Project `7e7dcb8bf808d87fcf1cc292ae4e478e63e6a37c` on 2026-09-26. Station
required accurate test-inventory/proxy-provenance limits, additional Python skip
detection and disabled rustup auto-install. Project required a permanent handoff
link; the link above now uses the corrected Station commit, surviving branch retirement.

The follow-up also narrows the Python import path, repairs ShellCheck trailing-reason
measurement, and removes an unverified database-age guarantee. The Station handoff
records the disposition. These corrections require a new exact-head delta review;
the earlier review is not approval of later commits. Other optional improvements
and future S3b/S4 requirements remain deferred. Owner acceptance is still pending.
