## Targetting Specific Nodes
In Ansible, you can target specific nodes or groups of nodes for executing tasks or playbooks. This is done using the inventory file and specifying the desired hosts when running Ansible commands.


### Using Inventory File
You can group your managed nodes in the inventory file to target specific sets of nodes.
For example, you can create groups like `[webservers]`, `[dbservers]`, etc., and assign nodes to these groups.

Example inventory file (inventory):
```sh
[webservers]
172.16.250.132
172.16.250.248

[db_servers]
172.16.250.133

[file_servers]
172.16.250.134

```
### Targeting Specific Groups in Playbooks
When writing playbooks, you can specify which group of nodes to target using the `hosts` directive.

Example playbook targeting the `webservers` group:
- we want to run updates on all nodes 
- install apache only on webservers
```yaml
---
- hosts: all
  become: yes
  tasks:


    - name: Install updates (CentOs)
      dnf:
        update_only: yes
        update_cache: yes
      when: ansible_distribution == "CentOS"
    
    - name: Install updates (Ubuntu)
      apt:
        upgrade: dist
        update_cache: yes
      when: ansible_distribution == "Ubuntu"


- hosts: webservers
  become: yes
  tasks:
    - name: Ensure Apache is installed
      apt:
        name: apache2
        state: present
      when: ansible_distribution == "Ubuntu"

    - name: Ensure httpd is installed
      dnf:
        name: httpd
        state: present
      when: ansible_distribution == "CentOS"      
```    


### Targeting Specific Nodes in Ad-Hoc Commands
You can target specific nodes or groups of nodes using the `-i` option to specify the inventory file and the `-l` option to limit the command to specific hosts or groups.
Example command to target a specific host:
```sh
ansible -i inventory
```
