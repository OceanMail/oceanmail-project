# Branch preservation guidance

The September 2026 cleanup established a general rule: branch ancestry alone is
not sufficient evidence for deletion when work may have been squash-merged,
rebased, partially incorporated or superseded.

For the current public repositories, inspect open PRs and compare unique commits
and file contents before retiring a branch. Preserve unfinished work unless its
disposition is explicit. An earlier inventory is not authority to delete a branch
created or changed since that inventory. See [AGENTS.md](../../AGENTS.md).
