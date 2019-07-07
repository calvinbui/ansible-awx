[![Build Status](https://travis-ci.com/calvinbui/ansible-awx.svg?branch=master)](https://travis-ci.com/calvinbui/ansible-awx)
![GitHub release](https://img.shields.io/github/release/calvinbui/ansible-awx.svg)
![Ansible Quality Score](https://img.shields.io/ansible/quality/35898.svg)
![Ansible Role](https://img.shields.io/ansible/role/d/35898.svg)

# Ansible AWX

Install AWX on Ubuntu via [Docker](https://github.com/ansible/awx/blob/devel/INSTALL.md#docker-or-docker-compose). This role expects dependencies to be installed already such as Docker, pip, nodejs and git.

Note: any modified files in the AWX repository will be discarded on each run.

##  Requirements

N/A

## Role Variables

`awx_repo_directory`: where to clone down the AWX repo

`awx_version`: [branch name](https://github.com/ansible/awx/branches) or [tag](https://github.com/ansible/awx/tags)

`awx_update_repo`: update the repo on each run. good for those on `devel` branch.

`awx_vars`: variables to replace defaults set in [here](https://github.com/ansible/awx/blob/devel/installer/inventory). Only `awx_postgres_data_dir` is recommended to be set. Create as many as needed.

## Dependencies

A [list of pre-requisites](https://github.com/ansible/awx/blob/devel/INSTALL.md#prerequisites) is provided on the AWX installation document.

The follow can install what is required:
```yaml
---
- hosts: all
  become: true
  vars:
    git_config: []
    pip_install_packages:
      - docker
      - ansible
    nodejs_version: 8
    nodejs_install_packages: []
  pre_tasks:
    - name: Update apt cache.
      apt:
        update_cache: true
        cache_valid_time: 600
      changed_when: false
  roles:
    - calvinbui.ansible_git
    - calvinbui.ansible_pip
    - calvinbui.ansible_nodejs
    - calvinbui.ansible_docker
```
## Example Playbook

See above. Add this role `calvinbui.ansible_awx` to it.

## License

GPLv3

## Author Information

http://calvin.me
