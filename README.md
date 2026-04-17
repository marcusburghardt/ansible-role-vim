Role Name
=========

This Ansible Role will ensure VIM is installed and configured according to user
preferences. Settings can be customized through variables. Take a look at the existing
defaults defined in `defaults/main.yml` and override them in a Playbook.

This role will:
- Ensure VIM is installed with enhanced packages and syntastic plugins;
- Ensure the proper settings in `~/.vim/vimrc`;
- Set VIM as the default `EDITOR` environment variable;

To install this role:
```
ansible-galaxy role install marcusburghardt.vim
```

Requirements
------------

- python3

Role Variables
--------------

You can customize your environment by editing variables in:
- `defaults/main.yml` -- user-facing defaults (recommended for customization)
- `vars/*.yml` -- OS-specific and task-specific variables (rarely changed)

Variables can also be set directly in your Playbook, which is the recommended approach
for per-environment customization. See the Example Playbook section.

### Task Control

The `vim_tasks` list controls which tasks are executed. Each entry has an `enabled`
flag and a `name` that maps to a task file in `tasks/`:

| Task | Description |
|------|-------------|
| `install_vim` | Installs VIM and syntastic plugins via OS packages |
| `configure_vim` | Configures `~/.vim/vimrc` settings and sets `EDITOR=vim` |

### VIM Configuration

The `vim_user_config` list defines vimrc settings managed via `lineinfile`. Each entry
supports `enabled`, `state` (present/absent), and `line` (the vimrc directive).

Default settings include:
- Filetype detection and syntax highlighting
- Incremental, case-smart search with highlighting
- Line numbers and cursor highlighting
- Tabs expanded to 4 spaces
- Command history (1000 entries)
- Wildmenu autocomplete with file type exclusions
- YAML-specific indentation and color scheme

Dependencies
------------

None.

Example Playbook
----------------

This playbook will prepare everything with the right variables.
For this example, lets call this playbook file as `ansible_vim.yml`:

```yaml
---
- hosts: linux
  vars:
    vim_tasks:
      - { enabled: true, name: 'install_vim' }
      - { enabled: true, name: 'configure_vim' }
  roles:
    - marcusburghardt.vim
```

Considering the inventory file is in the same folder and is called `hosts_vim`,
you can now run this command:
```
ansible-playbook -K -i hosts_vim ansible_vim.yml
```

License
-------

Licensed under the Apache License, Version 2.0.
See the [LICENSE](LICENSE) file for details.

Release Process
---------------

This project uses [release-please](https://github.com/googleapis/release-please) for
automated versioning and changelog generation. Commits to `main` must follow the
[Conventional Commits](https://www.conventionalcommits.org/) specification.

**How it works:**
1. Push commits to `main` using conventional prefixes (`feat:`, `fix:`, `chore:`, etc.)
2. Release-please automatically opens a PR with version bump and changelog updates
3. Merging the release PR creates a GitHub Release and tag
4. The Galaxy publish workflow automatically imports the new version to Ansible Galaxy

Author Information
------------------

Marcus Burghardt
- [https://buymeacoffee.com/marcusburghardt](https://buymeacoffee.com/marcusburghardt)
- [https://github.com/marcusburghardt](https://github.com/marcusburghardt)
- [https://www.linkedin.com/in/marcusburghardt](https://www.linkedin.com/in/marcusburghardt)
