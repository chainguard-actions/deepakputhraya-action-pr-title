<!-- markdownlint-disable -->

# Hardening Report: deepakputhraya--action-pr-title/v1.0.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **deepakputhraya--action-pr-title/v1.0.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/main.yml references two actions using mutable, non-SHA refs:
- `actions/checkout@master` (branch ref — can be silently updated to point to any commit)
- `actions/setup-node@v1` (tag ref — tags can be force-pushed)

Both should be pinned to a full 40-character commit SHA (e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # master`) to prevent supply-chain attacks.

Locations:

- `.github/workflows/main.yml:13`
- `.github/workflows/main.yml:14`

### missing-permissions (severity: medium)

The workflow file .github/workflows/main.yml has no top-level `permissions:` key and the single job (`build`) also has no job-level `permissions:` key. Without explicit permissions, the GITHUB_TOKEN is granted its default (often broad) permissions. A minimal permissions block such as `permissions: pull-requests: read` should be added at the top level or on the job.

Locations:

- `.github/workflows/main.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/main.yml: (1) Pinned actions/checkout@master to full SHA 61b9e3751b92087fd0b06925ba6dd6314e06f089 and actions/setup-node@v1 to full SHA f1f314fca9dfce2769ece7d933488f076716723e, preserving the original ref as a comment. (2) Added top-level `permissions: pull-requests: read` block — the minimal permission required for a PR title validation workflow.

