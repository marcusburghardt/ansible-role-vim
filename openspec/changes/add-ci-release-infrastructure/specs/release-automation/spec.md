## ADDED Requirements

### Requirement: Automated versioning from conventional commits

The repository SHALL use release-please to automatically determine version bumps based
on conventional commit messages pushed to the `main` branch. The `simple` release type
SHALL be used. Breaking changes (`feat!:`, `fix!:`, or `BREAKING CHANGE:` footer) SHALL
trigger a minor bump while below v2.0.0 (due to pre-major guards). Feature commits
(`feat:`) SHALL trigger a patch bump while below v2.0.0.

#### Scenario: Feature commit triggers patch bump

- **WHEN** a commit with prefix `feat:` is pushed to `main`
- **THEN** release-please opens a PR proposing a patch version bump

#### Scenario: Breaking change triggers minor bump

- **WHEN** a commit with `feat!:` prefix or `BREAKING CHANGE:` footer is pushed to `main`
- **THEN** release-please opens a PR proposing a minor version bump

#### Scenario: Non-conventional commit is ignored

- **WHEN** a commit without a conventional prefix is pushed to `main`
- **THEN** release-please does not include it in version bump calculations

### Requirement: Changelog generation

Release-please SHALL generate and maintain `CHANGELOG.md` with sections mapped to
conventional commit types: `feat` to Features, `fix` to Bug Fixes, `chore` to
Miscellaneous, `docs` to Documentation, `refactor` to Refactoring.

#### Scenario: Changelog sections populated from commits

- **WHEN** a release PR is created
- **THEN** the CHANGELOG.md is updated with entries grouped by commit type into the configured sections

### Requirement: GitHub Release creation

When a release-please PR is merged, a GitHub Release SHALL be created with a tag
in the format `vX.Y.Z` (no component prefix).

#### Scenario: Release PR merged

- **WHEN** the release-please version bump PR is merged to `main`
- **THEN** a GitHub Release is created with the corresponding `vX.Y.Z` tag

### Requirement: Release workflow configuration

The release workflow (`ci_release.yml`) SHALL run on pushes to `main`. It SHALL use
empty permissions at workflow level and grant `contents: write` and `pull-requests: write`
at job level. The release-please action SHALL be pinned by full commit SHA.

#### Scenario: Workflow triggers on main push

- **WHEN** a commit is pushed to the `main` branch
- **THEN** the `ci_release.yml` workflow runs the release-please action

#### Scenario: Workflow permissions are minimal

- **WHEN** the `ci_release.yml` workflow is inspected
- **THEN** workflow-level permissions are empty (`{}`) and job-level permissions are limited to `contents: write` and `pull-requests: write`

### Requirement: Release-please configuration files

The repository SHALL contain `release-please-config.json` with `simple` release type,
`include-component-in-tag: false`, pre-major bump guards enabled, and changelog section
mappings. The `.release-please-manifest.json` SHALL track the current version starting
at `1.0.0`.

#### Scenario: Configuration files present and valid

- **WHEN** the repository root is inspected
- **THEN** both `release-please-config.json` and `.release-please-manifest.json` exist with the specified configuration
