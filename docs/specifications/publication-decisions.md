# Publication decisions requiring owner input

> Current publication decision (2026-09-26): create fresh sanitized Project, Station and Desktop repositories with installed licenses. Preserve the original repositories privately under names ending in `-archive`. See `PUBLICATION.md` at the repository root. Earlier in-place conversion instructions and pending-license statements below are historical.


Status: **Code/docs license choices and zero required approvals approved 2026-09-25.** License installation, ownership/compatibility, contributor terms and administrative application remain pending.
These decisions block publication, not independent audit/remediation work.

## Licensing proposal

Recommended for OceanMail-owned application code: AGPL-3.0-only, subject to each
component's compatibility audit. Recommended for prose/specifications:
CC-BY-SA-4.0, with executable examples separately identified under the code
license. Preserve all third-party terms. Do not relicense Thunderbird, HERMES,
Mercury, copied code or assets under a blanket OceanMail notice.

| Candidate | Main consequence |
|---|---|
| Apache-2.0 | Permissive; proprietary derivatives possible; explicit contributor patent grant and patent-litigation termination. |
| MPL-2.0 | File-level source obligations on distribution; can coexist with proprietary separate files; contributor patent provisions. |
| GPL-3.0-only | Copyleft distribution obligations; remote use alone is not the AGPL network-source trigger; patent provisions. |
| AGPL-3.0-only | GPL-style copyleft plus source offer for users interacting remotely with modified covered software; patent provisions. |

All permit commercial use under their terms. None forces contributors to send
their improvements to OceanMail or prevents competing implementations. Code
license selection is not a freedom-to-operate determination. The AGPL proposal
fits the stated preference against closed downstream versions, and the owner approved this choice on 2026-09-25. No license file should be installed until ownership and the choice
are confirmed. Owner must also choose only versus or-later if changing this
proposal.

For names/logos, proposed policy is separate branding permission and no implied
endorsement of forks; attribution and truthful references remain permitted.
Confirm the actual rightsholder before asserting ownership. Artwork copyright
and trademark permissions need separate treatment; no assets are relicensed here.

## Contribution proposal

Recommend inbound=outbound plus DCO 1.1 sign-off for future contributions,
without copyright assignment or a separate CLA. Contributors retain copyright
and certify their right to submit. License patent grants come from the selected
license; DCO is a provenance certification, not a substitute patent license.
Do not retroactively forge sign-offs on existing commits. Existing authorship,
employment rights and third-party inputs still require review.

A CLA is an alternative if broader relicensing rights are deliberately wanted;
it is not necessary merely for forks/PRs. A formal Code of Conduct can follow;
respectful, relevant review and maintainer moderation suffice for preparation.

## Main protection proposal

Prepare main protection with required PRs, resolved conversations, current-base
required checks, no force pushes/deletion and administrator enforcement. Preserve
merge commits; do not require linear history. Proposed initial review count is
zero required human approvals so a sole maintainer can merge verified work;
maintainer review remains expected. Choose one if an independent human reviewer
will be available. Do not add an unavailable Code Owner or mandatory signing
requirement that would make normal recovery impossible. Any emergency rule change
must be logged and restored. No configuration is claimed applied.

## Exact decisions needed

1. Approve/replace the proposed code/docs licenses, branding separation and
   DCO/inbound=outbound terms; identify who can authorize existing first-party work.
2. Choose zero or one required human approval for main, with no routine bypass.
3. Apply the owner-approved privacy disposition: remove personal author metadata and private test/operational references. Current-tree edits alone are insufficient; history and GitHub surfaces remain gates. Sensitive values are intentionally not repeated here.
4. Enable a working private vulnerability-reporting route and provide administrative
   settings access/evidence for runners, Actions, membership and main protection.

## Primary references consulted 2026-09-25

- [Apache-2.0](https://www.apache.org/licenses/LICENSE-2.0), sections 3–6.
- [MPL-2.0](https://www.mozilla.org/en-US/MPL/2.0/), sections 2–3 and 5.
- [GPL-3.0](https://spdx.org/licenses/GPL-3.0-only.html), sections 6 and 11.
- [AGPL-3.0](https://spdx.org/licenses/AGPL-3.0-only.html), sections 11 and 13.
- [CC-BY-SA-4.0](https://creativecommons.org/licenses/by-sa/4.0/).
- [DCO 1.1](https://developercertificate.org/).
- [GitHub secure use](https://docs.github.com/en/actions/reference/security/secure-use).
