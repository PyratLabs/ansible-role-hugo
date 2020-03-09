# Ansible Role: Hugo

Ansible role for installing [Hugo](https://gohugo.io)

[![Build Status](https://www.travis-ci.org/PyratLabs/ansible-role-hugo.svg?branch=master)](https://www.travis-ci.org/PyratLabs/ansible-role-hugo)

## Requirements

This role has been tested on Ansible 2.7.0+ against the following Linux Distributions:

  - Amazon Linux 2
  - CentOS 8
  - CentOS 7
  - Debian 10
  - Fedora 29
  - Fedora 30
  - Fedora 31
  - Ubuntu 18.04 LTS

## Disclaimer

If you have any problems please create a GitHub issue, I maintain this role in
my spare time so I cannot promise a speedy fix delivery.

## Role Variables


| Variable                       | Description                                                               | Default Value    |
|--------------------------------|---------------------------------------------------------------------------|------------------|
| `hugo_version`                 | Use a specific version of Hugo, eg. `0.66.0`. Specify `false` for latest. | `false`          |
| `hugo_install_os_dependencies` | Allow role to install OS dependencies.                                    | `false`          |
| `hugo_install_dir`             | Installation directory for Hugo.                                          | `$HOME/bin`      |
| `hugo_projects_dir`            | Directory to put Hugo projects. Specify `false` to skip.                  | `$HOME/projects` |
| `hugo_projects`                | List of go projects to be cloned with `git`. See notes.                   | _NULL_           |


## Dependencies

No dependencies on other roles.

## Example Playbook

Example playbook for installing to single user:

```yaml
- hosts: workstation
  roles:
     - { role: xanmanning.hugo, hugo_version: 0.66.0 }
```

Example playbook for installing the latest hugo version globally:

```yaml
---
- hosts: workstation
  become: true
  vars:
    hugo_install_dir: /usr/local/bin
  roles:
    - role: xanmanning.hugo
```

### Note about `hugo_projects`

This is a list of git repositories to be cloned into the projects directory.
If this is empty, no projects will be cloned.

Below is an example of a project:

```yaml
hugo_projects:
    - name: myhugosite.com                            # Directory name to clone into
      repo: git@github.com:mygithub/myhugosite        # Repository to clone
      update_repo: true                               # Always update local copy of repo
      version:  master                                # Check out this version of the repo
      force: false                                    # Discard any existing working copy of the repo
      key_file: "{{ ansible_user_dir }}/.ssh/id_rsa"  # Key file to use to clone the repo
      recursive: true                                 # Include submodules in clone
```


## License

[BSD 3-clause](LICENSE.txt)

## Author Information

[Xan Manning](https://xanmanning.co.uk/)
