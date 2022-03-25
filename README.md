# ansible-install-packages

Using ansible to install main packages that we, sysadmin and devops currently use in a notebook format or ubuntu linux servers.

- Docker
- Docker Compose
- Podman
- Kubectl
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

Before running the playbook, it is necessary to edit the main.yml file, in the "defaults" directory, which is where you will put the versions of some services to be installed or pass the playbook call, with the --extra-vars parameter.

first case

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
second case

```bash
ansible-playbook -i hosts playbook.yml --extra-vars "kubectl_version=1.21.0-00"
```

Playbook example.

```bash
---
- name: running playbook
  hosts: <servers>
  gather_facts: true
  become: true
  roles:
    - role: role-install-packages
...
```

If you just want to update or install only some tool, you can use the existing tags and pass it in the playbook call.

To list all existing tags in the role.

```bash
ansible-playbook -i hosts playbook.yml --list-tags
```

terminal return

```bash
playbook: playbook.yml

  play #1 (lab): Executando playbook.   TAGS: []
      TASK TAGS: [docker, helm, kind, kubectl, remove-cache-ubuntu, terraform, update-ubuntu, upgrade-ubuntu, vagrant, install-packages-ubuntu]
```

To install only docker, use this: 

In this case, the playbook will understand and execute only the task that has "docker" as a tag.

```bash
ansible-playbook -i hosts playbook.yml --tags docker
```

So that you don't run some specific tool, do it like this:

In this case, the playbook will be executed and only the one tagged as docker will not be executed, all others will be executed.

```bash
ansible-playbook -i hosts playbook.yml --skip-tags docker
```


