# Publication decisions

Status: **ACTIVE — updated 2026-09-26**.

## Settled decisions

- All five components publish source: Project, Station, Desktop, Server and Infrastructure.
- OceanMail-owned code uses AGPL-3.0-only; documentation uses CC-BY-SA-4.0.
  License files are installed. [LICENSING.md](../../LICENSING.md) defines their scope;
  third-party code and assets keep their own terms.
- External contributors can read, fork and submit pull requests without organization
  membership or upstream write access. Maintainers decide acceptance and merges.
- Use protected `main`, required checks and zero required approving reviews.
  Preserve merge commits and do not bypass protection or force-push `main`.
- No DCO, CLA or additional inbound agreement is adopted. Do not manufacture sign-offs.
- Keep personal information, credentials and operational inventories out of public source.
- No patents by default; preserve technically meaningful public disclosures and upstream attribution.

## Continuing responsibilities

Review rights and provenance for new code, copied material and assets. Public
source licensing does not itself settle binary redistribution, branding/trademark
permissions, hosted-service operation or radio authorization. These remain
separate release decisions. See [publication-readiness.md](publication-readiness.md).

The external-fork acceptance test remains unverified. Administrative controls
must be reviewed when settings or workflows change; do not treat a passing source
check as proof of runner isolation or secret-access settings.
