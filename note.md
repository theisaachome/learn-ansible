## Create Inventory

add the node that we want to manage,
example:
```
localhost
176.10.256.23
176.10.256.24
```

add ansible.cfg file

```
[defaults]
inventory = inventory
private_key_file = ~/.ssh/ansible

```

command line 

```sh
ansible all -m gather_facts 
```

```sh
ansible all -m gather_facts --limit (ip-address)
```

### Running elevated ad-hoc Commands
by default, Ansible runs commands as the user you connect as (usually your local user). To run commands with elevated privileges, use the --become option.
Example:
```sh
ansible all -m command -a "whoami" --become
```

### Writing playbooks
Playbooks are files written in YAML format that define a series of tasks to be executed on your managed nodes.
Example playbook (site.yml):
```yaml
---
- hosts: all
  become: yes
    tasks:
        - name: Ensure Apache is installed
        apt:
            name: apache2
            state: present
        - name: Ensure Apache is running
        service:
            name: apache2
            state: started
            enabled: yes
```

### Running a playbook
To execute a playbook, use the ansible-playbook command followed by the playbook file name.
Example:
```sh
ansible-playbook site.yml
```