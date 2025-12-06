### The When Conditional
The `when` conditional in Ansible allows you to execute tasks only when certain conditions are met. This is useful for controlling the flow of your playbooks based on variables, facts, or other criteria.

#### Syntax
The basic syntax for using the `when` conditional is as follows:
```yaml
- name: Task name
  module_name:
    parameter: value
  when: condition
```

#### Example Usage
Here is an example of using the `when` conditional in a playbook:
```yaml---
- hosts: all
  tasks:
    - name: Install Apache on Debian-based systems
      apt:
        name: apache2
        state: present
      when: ansible_facts['os_family'] == "Debian"  
    - name: Install Apache on RedHat-based systems
      yum:
        name: httpd
        state: present
#      when: ansible_facts['os_family'] == "RedHat"
      when: ansible_distribution == "RedHat"
```