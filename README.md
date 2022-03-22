# ansible-install-packages

Using ansible to install main packages that we, sysadmin and devops currently use in a notebook format.

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

before running the playbook, it is necessary to edit the main.yml file, in the "defaults" directory, which is where you will put the versions of some services to be installed.

```bash
---
# defaults file for role-install-packages

# Variable kubectl version - example: 1.21.0-00
kubectl_version: 1.21.0-00

# Variable kind version - example: v0.12.0
kind_version: v0.12.0

# Variable helm version - example: v3.0.0
helm_version: v3.8.1

...
```


playbook example.

´´´bash
  ---
  
  - name: running playbook
    hosts: <servers>
    gather_facts: false
    become: true
    roles:
      - role: role-install-packages

´´´