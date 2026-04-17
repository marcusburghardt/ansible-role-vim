## Why

The repository has no CI/CD infrastructure, no automated release process, and is missing
essential project hygiene files (.gitignore, .yamllint, LICENSE). Without these, releases
are manual, YAML quality is unverified, and the project lacks the standard infrastructure
established across other roles in this collection (ansible-role-ai, ansible-role-git).

## What Changes

- Add GitHub Actions workflow for automated versioning and changelog generation via release-please
- Add GitHub Actions workflow for automated Ansible Galaxy publishing on release
- Add Dependabot configuration for GitHub Actions dependency monitoring
- Add `.yamllint` configuration for consistent YAML linting
- Add root `.gitignore` for tool-managed and local-only files
- Add `LICENSE` file (Apache-2.0)
- Add `CHANGELOG.md` as initial changelog managed by release-please
- Add `release-please-config.json` and `.release-please-manifest.json`
- **BREAKING**: Change license from MPL-2.0 to Apache-2.0
- Update `meta/main.yml` to reflect Apache-2.0 license
- Update `README.md` with release process documentation, improved variable docs, and author links

## Capabilities

### New Capabilities

- `release-automation`: Automated versioning and changelog generation from conventional commits via release-please
- `galaxy-publishing`: Automated Ansible Galaxy role publishing triggered by GitHub Releases
- `dependency-management`: Automated dependency update monitoring via Dependabot
- `project-hygiene`: Essential project files (.gitignore, .yamllint, LICENSE, CHANGELOG.md)

### Modified Capabilities

_(none -- no existing specs)_

## Impact

- **New files**: 9 files added (.github/workflows/ci_release.yml, .github/workflows/ci_galaxy_publish.yml, .github/dependabot.yml, .yamllint, .gitignore, release-please-config.json, .release-please-manifest.json, LICENSE, CHANGELOG.md)
- **Updated files**: 2 files modified (README.md, meta/main.yml)
- **Secrets required**: `GALAXY_API_KEY` must be configured in repository settings
- **Process change**: Commits to main must follow Conventional Commits specification going forward
- **License change**: MPL-2.0 to Apache-2.0 is a breaking change for downstream consumers
