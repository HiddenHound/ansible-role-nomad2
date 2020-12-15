# [nomad](#nomad)

Install and configure Nomad.

|Travis|GitHub|GitLab|Quality|Downloads|Version|
|------|------|------|-------|---------|-------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-nomad.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-nomad)|[![github](https://github.com/robertdebock/ansible-role-nomad/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-nomad/actions)|[![gitlab](https://gitlab.com/robertdebock/ansible-role-nomad/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-nomad)|[![quality](https://img.shields.io/ansible/quality/51615)](https://galaxy.ansible.com/robertdebock/nomad)|[![downloads](https://img.shields.io/ansible/role/d/51615)](https://galaxy.ansible.com/robertdebock/nomad)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-nomad.svg)](https://github.com/robertdebock/ansible-role-nomad/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.nomad
```

The machine needs to be prepared in CI this is done using `molecule/resources/prepare.yml`:
```yaml
---
- name: Prepare
  hosts: all
  gather_facts: no
  become: yes

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.core_dependencies
    - role: robertdebock.hashicorp
      hashicorp_products:
        - name: nomad
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for nomad

# Set this to "yes" for a server.
nomad_server: yes

# Configuration items for the Nomad server
nomad_server_data_dir: /tmp/server
nomad_server_bind_addr: 0.0.0.0
nomad_server_log_level: INFO

# How many servers and agents are expected?
nomad_server_bootstrap_expect: 1

# This this to "yes" for an agent.
nomad_agent: no

# Configuration items for the Nomad agent
nomad_agent_log_level: INFO
nomad_agent_data_dir: /tmp/agent
nomad_agent_name: "{{ inventory_hostname }}"

nomad_agent_port: 5656

nomad_agent_servers:
  - name: 127.0.0.1
    port: 4647
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/robertdebock/ansible-role-nomad/blob/master/requirements.txt).

## [Status of requirements](#status-of-requirements)

The following roles are used to prepare a system. You may choose to prepare your system in another way, I have tested these roles as well.

| Requirement | Travis | GitHub |
|-------------|--------|--------|
| [robertdebock.bootstrap](https://galaxy.ansible.com/robertdebock/bootstrap) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-bootstrap.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-bootstrap) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-bootstrap/actions) |
| [robertdebock.core_dependencies](https://galaxy.ansible.com/robertdebock/core_dependencies) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-core_dependencies.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-core_dependencies) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-core_dependencies/actions) |
| [robertdebock.hashicorp](https://galaxy.ansible.com/robertdebock/hashicorp) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-hashicorp.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-hashicorp) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-hashicorp/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-hashicorp/actions) |

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/nomad.png "Dependency")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|el|7, 8|
|debian|buster|
|fedora|32, 33|
|ubuntu|bionic, focal|

The minimum version of Ansible required is 2.9, tests have been done to:

- The previous version.
- The current version.
- The development version.



## [Testing](#testing)

[Unit tests](https://travis-ci.com/robertdebock/ansible-role-nomad) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-nomad/issues)

Testing is done using [Tox](https://tox.readthedocs.io/en/latest/) and [Molecule](https://github.com/ansible/molecule):

[Tox](https://tox.readthedocs.io/en/latest/) tests multiple ansible versions.
[Molecule](https://github.com/ansible/molecule) tests multiple distributions.

To test using the defaults (any installed ansible version, namespace: `robertdebock`, image: `fedora`, tag: `latest`):

```
molecule test

# Or select a specific image:
image=ubuntu molecule test
# Or select a specific image and a specific tag:
image="debian" tag="stable" tox
```

Or you can test multiple versions of Ansible, and select images:
Tox allows multiple versions of Ansible to be tested. To run the default (namespace: `robertdebock`, image: `fedora`, tag: `latest`) tests:

```
tox

# To run CentOS (namespace: `robertdebock`, tag: `latest`)
image="centos" tox
# Or customize more:
image="debian" tag="stable" tox
```

## [License](#license)

Apache-2.0


## [Author Information](#author-information)

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
