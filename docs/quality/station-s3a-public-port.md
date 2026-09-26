# Station S3a public port — 2026-09-26

[Station PR #4](https://github.com/OceanMail/oceanmail-station/pull/4) and
[Project PR #4](https://github.com/OceanMail/oceanmail-project/pull/4) merged on
2026-09-26. S3a adds quality tooling and tracking; it does not activate a
production baseline or CI enforcement.

## Scope and preservation

The Station changes add quality adapters, tests, hash-locked tooling and the
selected Rust 1.98.1 toolchain. Product source, HERMES/Mercury selections,
the retirement regression patch and existing acceptance workflows are preserved.
The public PRs record exact bases, final heads and validation runs. Earlier
measurements remain historical and do not validate current commits.

## Review and evidence

Implementation details and reproduction commands belong in Station's
[current S3a handoff](https://github.com/OceanMail/oceanmail-station/blob/main/.quality/S3A-HANDOFF.md).
The [handoff snapshot after status reconciliation](https://github.com/OceanMail/oceanmail-station/blob/df2b438c5a466116032011b935887fb84d4b56b3/.quality/S3A-HANDOFF.md)
provides a permanent reference that survives branch retirement.

Claude independently reviewed Station `8fa010c24beb2b639350991a21ed14406f1c633c`
and Project `7e7dcb8bf808d87fcf1cc292ae4e478e63e6a37c` on 2026-09-26. Corrections
document test-inventory/proxy-provenance limits, detect more Python skip forms,
disable rustup auto-install, narrow the Python import path, repair ShellCheck
trailing-reason measurement and remove an unverified database-age guarantee.
Project adds the permanent handoff link. The public PRs record fresh validation
on their final heads, including passing Station integration checks.

The public merge records document the owner's 2026-09-26 instruction to finish
using that completed review without another Claude pass. No independent Claude
review of the later correction commits is claimed. The normal exact-head review
requirement remains for future retrofit work; this was a specific closeout exception.

STATIC / UNIT comprises tooling tests, scanner fixture probes and report-only
measurement. Existing hosted no-radio acceptance is INTEGRATION. There is no
LIVE / PRODUCT, physical-radio or production-security claim. Report-only findings
remain; no production suppression/advisory ledger, baseline, required quality
workflow or protection setting is introduced. S3b/S4 require separate assignment.
