Role Name
=========

This Ansible Role will ensure the VIM is installed and configured according to the user
preferences. Settings can be customized through variables. Take a look in the existing
standards defined in "defaults/main.yml" and overridden them in a Playbook.

This role will:
- Ensure VIM is installed;
- Ensure the proper settings in ~/.vim/vimrc;

To install this role:  
```$ ansible-galaxy role install marcusburghardt.vim```

Requirements
------------

- python3

Role Variables
--------------

You can customize your environment in a very simple and centralized way editing some variables in:
- defaults/main.yml

In some rare cases, you may change some configuration to reflect your local environment in:
- vars/*.yml

Observe that the above variables could be set in your Playbook too, which, IMO is much more elegant. ;)  
Take a look in the Example Playbook section.

Dependencies
------------

None.

Example Playbook
----------------

This playbook will prepare everything with the right variables.  
For this example, lets call this playbook file as "ansible_vim.yml":

```
---
- hosts: linux
  vars:
    - git_tasks:
      - { enabled: true,  name: 'install_vim' }
      - { enabled: true,  name: 'configure_vim' }
  roles:
    - marcusburghardt.vim
```

Considering the inventory file is in the same folder and is called "hosts_git",
you can now run this command:  
```$ ansible-playbook -K -i hosts_vim ansible_vim.yml```

License
-------

This Source Code Form is subject to the terms of the Mozilla Public
License, v. 2.0. If a copy of the MPL was not distributed with this
file, You can obtain one at http://mozilla.org/MPL/2.0/.

Author Information
------------------

Marcus Burghardt
- [https://buymeacoffee.com/marcusburghardt](https://buymeacoffee.com/marcusburghardt)
- [https://github.com/marcusburghardt](https://github.com/marcusburghardt)
- [https://www.linkedin.com/in/marcusburghardt](https://www.linkedin.com/in/marcusburghardt)
