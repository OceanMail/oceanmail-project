# Public repository administration

Updated 2026-09-26: all five repositories are public with protected `main` branches.
This is an ongoing maintenance checklist, not a request to change visibility.

- Keep public PR execution on GitHub-hosted runners; exclude trusted runners at the access boundary.
- Keep Actions tokens read-only and secrets/write tokens unavailable to untrusted PR code.
- Review collaborator, app, deploy-key and environment access when configuration changes.
- Maintain private vulnerability reporting as described in each repository's SECURITY.md.
- Require current-base checks and PRs; preserve merge commits and zero required approving reviews.
- Verify protection and public Actions results after changes. Never bypass protection to clear a failure.

| Repository | Required check names |
|---|---|
| Project | docs |
| Station | auth, phase3a, phase4i |
| Desktop | lint |
| Server | docs |
| Infrastructure | docs |

An end-to-end external-fork test remains unverified. Use a real non-write contributor
to confirm fork/PR/review access, GitHub-hosted validation without secrets or useful
write tokens, denied upstream push/merge, and maintainer integration. Same-repository
CI cannot establish this result. Record findings without personal or operational data.
