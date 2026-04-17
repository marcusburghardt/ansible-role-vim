## 1. Project Hygiene Files

- [x] 1.1 Create root `.gitignore` with SpecKit, OpenCode, and agent ignore patterns
- [x] 1.2 Create `.yamllint` configuration extending default with project rules
- [x] 1.3 Create `LICENSE` file with full Apache License, Version 2.0 text
- [x] 1.4 Create initial `CHANGELOG.md` with v1.0.0 entry documenting existing features and infrastructure changes
- [x] 1.5 Update `meta/main.yml` license from MPL to Apache-2.0

## 2. Release-Please Configuration

- [x] 2.1 Create `release-please-config.json` with simple release type, pre-major bump guards, and changelog sections
- [x] 2.2 Create `.release-please-manifest.json` with starting version 1.0.0
- [x] 2.3 Create `.github/workflows/ci_release.yml` with release-please action (SHA-pinned, least-privilege permissions)

## 3. Galaxy Publishing

- [x] 3.1 Create `.github/workflows/ci_galaxy_publish.yml` with Galaxy import triggered on release (SHA-pinned actions, least-privilege permissions)

## 4. Dependency Management

- [x] 4.1 Create `.github/dependabot.yml` for weekly GitHub Actions monitoring with conventional commit prefix

## 5. Documentation

- [x] 5.1 Update `README.md` with Apache-2.0 license reference, release process section, improved variable documentation, and author links
