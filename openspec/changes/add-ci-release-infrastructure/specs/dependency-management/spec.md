## ADDED Requirements

### Requirement: Dependabot monitors GitHub Actions

Dependabot SHALL be configured to monitor the `github-actions` ecosystem for dependency
updates with a weekly schedule.

#### Scenario: Weekly update check

- **WHEN** a week has passed since the last Dependabot check
- **THEN** Dependabot checks for updated versions of all GitHub Actions used in workflows

#### Scenario: Update PR created

- **WHEN** a newer version of a GitHub Action is available
- **THEN** Dependabot opens a PR to update the action reference

### Requirement: Conventional commit format for Dependabot PRs

Dependabot commit messages SHALL use the `chore` prefix with scope included, following
the conventional commits format expected by release-please.

#### Scenario: Commit message format

- **WHEN** Dependabot creates an update PR
- **THEN** the commit message uses the format `chore(deps): bump <action> from <old> to <new>`
