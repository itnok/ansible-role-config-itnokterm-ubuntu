config-itnokterm-ubuntu
=======================

[![Build Status](https://travis-ci.org/itnok/ansible-role-config-itnokterm-ubuntu.svg?branch=master)](https://travis-ci.org/itnok/ansible-role-config-itnokterm-ubuntu) [![GitHub tag](https://img.shields.io/github/v/tag/itnok/ansible-role-config-itnokterm-ubuntu?sort=semver)](https://github.com/itnok/ansible-role-config-itnokterm-ubuntu/tags/) [![Ansible Role](https://img.shields.io/ansible/role/48400)](https://galaxy.ansible.com/itnok/config_itnokterm_ubuntu)

Clone itnok-term GitHub repo in user's $HOME and configure the account to use it.

Steps performed are:

  - Using role [itnok.manage_pkg_ubuntu](https://galaxy.ansible.com/itnok/manage_pkg_ubuntu):
    * Make sure git, vim, tmux, xclip, dconf-cli, alacritty, emacs-nox, python3-pip and python3-psutil packages are installed
  - Make sure `~/.ssh` directory exists
  - Install provided deploy key for itnok-term
  - Make sure `~/.custom` directory exists
  - Clone `itnok-term` repository in `~/.custom`
  - Install NVM v0.35.3 & Node.js v12.16.2
  - Install Powerline modules
  - Create symbolic links for all needed files in $HOME _(:warning: it **OVERWRITES** data eventually present!)_
  - Add custom Gnome Terminal profile
  - Read current list of Gnome Terminal profiles
  - Create new list of Gnome Trminal profiles adding the one from `itnok-term`
  - Make `itnok-term` profile the default for Gnome Terminal


## :exclamation: Requirements
-----------------------------

None.


## :abcd: Role Variables
------------------------

| Variable                              | Description                                         | Default Value                          |
|---------------------------------------|-----------------------------------------------------|----------------------------------------|
| `config_itnokterm_gterm_profile_uuid` | Gnome Terminal UUID to use as default               | `1311470c-c450-1073-773b-e11ee50de666` |
| `config_itnokterm_git_deploy_key`     | GitHub deploy key to use (itnok-term is private)    | `None`                                 |
| `config_itnokterm_user`               | User to configure on the target Ubuntu system       | `root`                                 |
| `config_itnokterm`                    | Version/branch of itnok-term to install             | `master`                               |


## :link: Dependencies
----------------------

- [itnok.manage_pkg_ubuntu](https://galaxy.ansible.com/itnok/manage_pkg_ubuntu) _(:octocat: [ansible-role-manage-pkg-ubuntu](https://github.com/itnok/ansible-role-manage-pkg-ubuntu))_
- [itnok.install_nvm_ubuntu](https://galaxy.ansible.com/itnok/install_nvm_ubuntu) _(:octocat: [ansible-role-install-nvm-ubuntu](https://github.com/itnok/ansible-role-install-nvm-ubuntu))_

To install dependencies use:
```
    $ ansible-galaxy install <dependecy.name>
```

Installation of the required Ansible Roles can also be simply addressed with:
```
    $ ansible-galaxy install -r requirements.yml
```


## :notebook: Example Playbook
------------------------------

Here an example of how to use this role in your playbooks:

```
---
- hosts: servers
  remote_user: ubuntu   # optional (your remote user)
  gather_facts: yes     # optional
  become: yes

  roles:
    - { role: itnok.config_itnokterm_ubuntu }

  vars:
    config_itnokterm_user: "ubuntu"
    config_itnokterm_git_deploy_key: "<SOME_LONG_STRING_FROM_YOUR_VAULT_HERE>"
    config_itnokterm: "master"
```

## :guardsman: License
----------------------

MIT _([read more](LICENSE.md))_
