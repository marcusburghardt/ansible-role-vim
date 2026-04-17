## ADDED Requirements

### Requirement: Root .gitignore

The repository SHALL have a root `.gitignore` file that excludes tool-managed
infrastructure (SpecKit caches, OpenCode plugin artifacts), local agent directories
(.cursor, .claude), and agent-specific files (CLAUDE.md).

#### Scenario: Tool artifacts ignored

- **WHEN** OpenCode plugin installs node_modules or generates package files in `.opencode/`
- **THEN** these files are excluded from version control by `.gitignore`

#### Scenario: Agent directories ignored

- **WHEN** `.cursor/`, `.claude/`, or `CLAUDE.md` files are present locally
- **THEN** they are excluded from version control by `.gitignore`

### Requirement: YAML lint configuration

The repository SHALL have a `.yamllint` configuration file that extends the default
ruleset with: `line-length` max 200 (warning level), `truthy` allowing only `'true'`
and `'false'`, `comments` requiring starting space with 1 min space from content,
`braces` with max 1 space inside, and `octal-values` forbidding implicit octals.
The `.opencode/` and `openspec/` directories SHALL be ignored.

#### Scenario: Lint configuration present and valid

- **WHEN** `.yamllint` is inspected
- **THEN** it contains the specified rules and ignore patterns

#### Scenario: Tool directories excluded from linting

- **WHEN** yamllint runs against the repository
- **THEN** files in `.opencode/` and `openspec/` are not checked

### Requirement: LICENSE file

The repository SHALL contain a `LICENSE` file with the full Apache License, Version 2.0
text. The license in `meta/main.yml` SHALL be `Apache-2.0`. The README SHALL reference
Apache-2.0 and link to the LICENSE file.

#### Scenario: License consistency

- **WHEN** the LICENSE file, meta/main.yml, and README.md are inspected
- **THEN** all three consistently reference Apache-2.0

#### Scenario: Breaking change documented

- **WHEN** the CHANGELOG.md for v1.0.0 is inspected
- **THEN** the license change from MPL-2.0 to Apache-2.0 is documented

### Requirement: Initial CHANGELOG.md

The repository SHALL contain a `CHANGELOG.md` with an initial v1.0.0 entry documenting
existing role features and the infrastructure added by this change. Release-please SHALL
manage this file for subsequent releases.

#### Scenario: Initial entry present

- **WHEN** `CHANGELOG.md` is inspected
- **THEN** it contains a v1.0.0 section with Features and Miscellaneous subsections

#### Scenario: Release-please manages future entries

- **WHEN** a new release-please PR is merged
- **THEN** CHANGELOG.md is updated automatically with new version entries
