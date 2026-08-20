<!-- markdownlint-disable -->

# Hardening Report: mikepenz--action-junit-report/v6.3.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mikepenz--action-junit-report/v6.3.1** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple `uses:` references in build.yml are pinned to mutable tags rather than full 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks if those tags are moved. Unpinned references found:
- `actions/checkout@v6` (lines 14, 30, 75)
- `actions/setup-node@v6` (lines 15, 31)
- `mikepenz/release-changelog-builder-action@v6` (line 79)
- `mikepenz/action-gh-release@v1` (line 87)

Locations:

- `.github/workflows/build.yml:14`
- `.github/workflows/build.yml:15`
- `.github/workflows/build.yml:30`
- `.github/workflows/build.yml:31`
- `.github/workflows/build.yml:75`
- `.github/workflows/build.yml:79`
- `.github/workflows/build.yml:87`

### unpinned-uses (severity: high)

Multiple `uses:` references in codeql-analysis.yml are pinned to mutable tags rather than full 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks if those tags are moved. Unpinned references found:
- `actions/checkout@v6` (line 37)
- `github/codeql-action/init@v4` (line 41)
- `github/codeql-action/autobuild@v4` (line 51)
- `github/codeql-action/analyze@v4` (line 54)

Locations:

- `.github/workflows/codeql-analysis.yml:37`
- `.github/workflows/codeql-analysis.yml:41`
- `.github/workflows/codeql-analysis.yml:51`
- `.github/workflows/codeql-analysis.yml:54`

### missing-permissions (severity: medium)

build.yml has no top-level `permissions:` key and none of its three jobs (`build`, `test`, `release`) define a `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be broader than necessary (e.g. write access to contents and pull requests). Each job should declare the minimal permissions it requires.

Locations:

- `.github/workflows/build.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all findings in both workflow files:

**build.yml**:
- Pinned actions/checkout@v6 to @d23441a48e516b6c34aea4fa41551a30e30af803 (3 occurrences)
- Pinned actions/setup-node@v6 to @249970729cb0ef3589644e2896645e5dc5ba9c38 (2 occurrences)
- Pinned mikepenz/release-changelog-builder-action@v6 to @c9bcd8238b6f41e05561348339429d360b1c0247
- Pinned mikepenz/action-gh-release@v1 to @9a604afa5167a745eab07256a54e2f578a1a0c5e
- Added top-level `permissions: {}` to deny all by default
- Added per-job permissions: build (contents: read), test (contents: read, checks: write, pull-requests: write), release (contents: write)

**codeql-analysis.yml**:
- Pinned actions/checkout@v6 to @d23441a48e516b6c34aea4fa41551a30e30af803
- Pinned github/codeql-action/init@v4 to @ff2f1c621b7f889edc0d3c761ac2e6a3f8cdb0dd
- Pinned github/codeql-action/autobuild@v4 to @ff2f1c621b7f889edc0d3c761ac2e6a3f8cdb0dd
- Pinned github/codeql-action/analyze@v4 to @ff2f1c621b7f889edc0d3c761ac2e6a3f8cdb0dd
- (codeql-analysis.yml already had a permissions block in the analyze job, no change needed there)

