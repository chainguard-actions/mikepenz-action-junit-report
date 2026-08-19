<!-- markdownlint-disable -->

# Hardening Report: mikepenz--action-junit-report/v6.4.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mikepenz--action-junit-report/v6.4.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Commit rebuilt dist' run: block in the commit-dist job directly interpolates GitHub Actions expressions into a shell command string (rule a). Specifically, `${{ github.repository }}` and `${{ github.event.pull_request.head.ref }}` are embedded directly in the `git push` URL, and `${{ secrets.RENOVATE_TOKEN }}` is embedded in the command. These values undergo YAML template substitution before the shell processes them, allowing an attacker who controls the PR branch name or repository name to inject shell metacharacters. The offending line is: `git push https://x-access-token:${{ secrets.RENOVATE_TOKEN }}@github.com/${{ github.repository }}.git HEAD:${{ github.event.pull_request.head.ref }}`

Locations:

- `.github/workflows/build.yml:56`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection

**Notes:**

Fixed script injection in .github/workflows/build.yml at the 'Commit rebuilt dist' step. Moved `${{ secrets.RENOVATE_TOKEN }}`, `${{ github.repository }}`, and `${{ github.event.pull_request.head.ref }}` out of the `run:` shell string and into the step's `env:` block as RENOVATE_TOKEN, REPOSITORY, and HEAD_REF respectively. The `git push` command now references these as plain shell variables (${RENOVATE_TOKEN}, ${REPOSITORY}, ${HEAD_REF}), preventing shell metacharacter injection from attacker-controlled values like the PR branch name.

