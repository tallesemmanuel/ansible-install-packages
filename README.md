# ansible-install-packages

Using ansible to install main packages that we, sysadmin and devops currently use in a notebook format or ubuntu linux servers.

- Docker
- Kubectl
- Ansible
- Terraform
- Vagrant
- Kind
- Helm

## Requirements

- Ubuntu 20.04.4 LTS. But it could be another version.

- Ssh key on the target server.

## How to do the whole procedure

Download the project.

```bash
git clone https://github.com/tallesemmanuel/ansible-install-packages.git
```

Before running the playbook, it is necessary to edit the main.yml file, in the "defaults" directory, which is where you will put the versions of some services to be installed.

```bash
---
# defaults file for role-install-packages

# Variable kubectl version - example: 1.21.0-00
kubectl_version: 1.21.0-00

# Variable kind version - example: v0.12.0
kind_version: v0.12.0

# Variable helm version - example: v3.0.0
helm_version: v3.8.1

# Variable vagrant version - example: 2.2.18
vagrant_version: 2.2.17

...
```


If you don't want to install any of these tools, just comment out the desired line in the main.yml file, in the "tasks" directory.

Example: I just want to update my ubuntu and install docker, in this case I can comment the others.

```bash
---
# tasks file for role-install-packages


- include: update-upgrade-ubuntu.yml
- include: install-docker-ubuntu.yml
#- include: install-terraform-ubuntu.yml
#- include: install-kubectl-ubuntu.yml
#- include: install-kind-ubuntu.yml
#- include: install-vagrant-ubuntu.yml
...
```


Playbook example.

```bash
---
- name: running playbook
  hosts: <servers>
  gather_facts: false
  become: true
  roles:
    - role: role-install-packages
...
```