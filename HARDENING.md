<!-- markdownlint-disable -->

# Hardening Report: mikepenz--action-junit-report/v6.5.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mikepenz--action-junit-report/v6.5.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### broad-permissions (severity: medium)

The workflow file scorecard.yml has a top-level `permissions: read-all` setting, which grants overly broad read access to all scopes. This should be replaced with specific minimal permissions required by each job.

Locations:

- `.github/workflows/scorecard.yml:10`

## Iteration Notes

### Iteration 1

**Fixes applied:** broad-permissions

**Notes:**

Replaced top-level `permissions: read-all` in .github/workflows/scorecard.yml with specific minimal permissions `contents: read`. The job-level permissions block already defines the specific write permissions needed (`security-events: write` and `id-token: write`), so the top-level only needs `contents: read` for the checkout step.

