## Context

ansible-role-vim is a minimal Ansible role (4 commits, no tags) that installs and configures
VIM. It currently has no CI/CD, no release process, and is missing standard project hygiene
files. The same infrastructure pattern has been successfully applied to ansible-role-git and
ansible-role-ai, providing a proven template to follow.

The role is published on Ansible Galaxy as `marcusburghardt.vim` but releases are entirely
manual. The license is declared as MPL-2.0 in meta/main.yml and README but no LICENSE file
exists.

## Goals / Non-Goals

**Goals:**

- Establish automated release process matching the pattern used in ansible-role-git
- Automate Ansible Galaxy publishing on release
- Add dependency monitoring for GitHub Actions
- Add project hygiene files (.gitignore, .yamllint, LICENSE, CHANGELOG.md)
- Improve README with release process documentation and better variable coverage
- Standardize license as Apache-2.0 (consistent with other roles)

**Non-Goals:**

- CI linting workflow (yamllint, ansible-lint gates) -- future improvement
- CI testing workflow (molecule) -- future improvement
- Debian/Ubuntu platform support -- separate concern
- Pre-commit hooks -- future improvement
- Makefile -- future improvement

## Decisions

### 1. Release type: `simple`

Use release-please's `simple` release type, which tracks version in
`.release-please-manifest.json` and generates changelog from conventional commits.

**Rationale**: Ansible roles are not language-specific packages. The `simple` type avoids
assumptions tied to node, python, or other ecosystems.

**Alternatives considered**: `node` (unnecessary package.json), `python` (unnecessary
setup.py/pyproject.toml).

### 2. Starting version: v1.0.0

Begin at version 1.0.0 rather than 0.x.

**Rationale**: The role is functional and has been available on Galaxy. Starting at 1.0.0
signals stability and aligns with ansible-role-git's approach. All existing (non-conventional)
commits predate the release-please configuration and won't trigger unintended version bumps.

**Alternatives considered**: v0.1.0 (would suggest the role is experimental, which doesn't
match reality).

### 3. Pre-major bump guards enabled

Set `bump-minor-pre-major: true` and `bump-patch-for-minor-pre-major: true`.

**Rationale**: Conservative versioning. While the role is at 1.x, breaking changes bump
minor and features bump patch. This prevents premature major version jumps during the
early stages of adopting conventional commits.

### 4. License: Apache-2.0

Switch from MPL-2.0 to Apache-2.0.

**Rationale**: Consistency with ansible-role-git and ansible-role-ai. Apache-2.0 is more
permissive and widely adopted in the Ansible ecosystem. Since no LICENSE file existed
previously (only a reference in meta/README), the practical impact is low.

**Alternatives considered**: Keep MPL-2.0 (creates inconsistency across roles), MIT (less
explicit patent grant than Apache-2.0).

### 5. Dependabot: github-actions only

Monitor only the `github-actions` ecosystem, not `pip`.

**Rationale**: The only pip dependency (ansible-core) is pinned in the workflow for
reproducibility and should be updated deliberately, not automatically. GitHub Actions
are safe to update automatically since they are pinned by SHA.

### 6. SHA-pinned GitHub Actions

All third-party actions are pinned by full commit SHA with version comments.

**Rationale**: Prevents supply chain attacks through tag mutation. The version comment
preserves human readability.

### 7. Workflow permissions: least privilege

Set empty permissions at workflow level (`permissions: {}`), then grant minimal
permissions at job level.

**Rationale**: Follows the principle of least privilege. Each job declares exactly
what it needs -- `contents: write` + `pull-requests: write` for release-please,
`contents: read` for Galaxy publish.

## Risks / Trade-offs

- **Breaking license change** → Document clearly in CHANGELOG and README. Practical
  impact is low since no LICENSE file previously existed.

- **Conventional commits adoption** → All future commits to main must follow the
  convention. Non-conforming commits are silently ignored by release-please (no
  breakage, just no version bump).

- **GALAXY_API_KEY secret required** → Galaxy publishing will fail silently if the
  secret is not configured. Must be set up in repository settings before first release.

- **No CI linting gate** → YAML and Ansible lint issues won't block merges. This is
  a known gap, accepted as a future improvement to keep this change focused.
