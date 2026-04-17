## ADDED Requirements

### Requirement: Automated Galaxy publishing on release

The repository SHALL automatically publish the role to Ansible Galaxy when a GitHub
Release is published. The workflow SHALL be triggered by `release: published` events,
chaining from the release-please workflow.

#### Scenario: Release triggers Galaxy import

- **WHEN** a GitHub Release is published (by release-please or manually)
- **THEN** the `ci_galaxy_publish.yml` workflow runs and imports the role to Ansible Galaxy

#### Scenario: Galaxy import uses correct namespace and role name

- **WHEN** the Galaxy import command executes
- **THEN** it uses `github.repository_owner` as namespace and `github.event.repository.name` as role name

### Requirement: Galaxy API authentication

The Galaxy publish workflow SHALL authenticate using a `GALAXY_API_KEY` secret. The
secret MUST be configured in repository settings before the first release.

#### Scenario: Authentication via secret

- **WHEN** the Galaxy import step runs
- **THEN** it passes the `GALAXY_API_KEY` secret as the `--token` argument

#### Scenario: Missing secret causes failure

- **WHEN** `GALAXY_API_KEY` is not configured in repository settings
- **THEN** the Galaxy import step fails

### Requirement: Workflow security

The Galaxy publish workflow SHALL use empty permissions at workflow level and grant only
`contents: read` at job level. All third-party actions SHALL be pinned by full commit SHA
with version comments.

#### Scenario: Least-privilege permissions

- **WHEN** the `ci_galaxy_publish.yml` workflow is inspected
- **THEN** workflow-level permissions are empty and job-level permissions are `contents: read` only

#### Scenario: Actions are SHA-pinned

- **WHEN** the workflow `uses` directives are inspected
- **THEN** all third-party actions reference a full 40-character commit SHA with a version comment

### Requirement: Python and ansible-core setup

The Galaxy publish workflow SHALL set up Python 3.12 and install `ansible-core==2.17.8`
to provide the `ansible-galaxy` command.

#### Scenario: Correct tool versions

- **WHEN** the workflow environment is inspected during execution
- **THEN** Python 3.12 and ansible-core 2.17.8 are installed
