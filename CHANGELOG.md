# Changelog

## [1.1.0](https://github.com/marcusburghardt/ansible-role-vim/compare/v1.0.0...v1.1.0) (2026-04-17)


### Features

* add CI/CD release infrastructure and project hygiene files ([991843a](https://github.com/marcusburghardt/ansible-role-vim/commit/991843aa2347a925dfc3dc5a0e120e4c74921903))

## [1.0.0](https://github.com/marcusburghardt/ansible-role-vim/releases/tag/v1.0.0) (2026-04-17)

### Features

* Install VIM with enhanced packages and syntastic plugins
* Configure ~/.vim/vimrc with data-driven settings (filetype detection, search, line numbers, tabs, history, wildmenu, YAML support)
* Set default EDITOR environment variable to vim

### Miscellaneous

* Add CI/CD infrastructure with release-please and Galaxy publishing
* Add Dependabot for GitHub Actions dependency updates
* Add `.yamllint` configuration for consistent YAML linting
* Switch license from MPL-2.0 to Apache-2.0
