## Playbook Note

This playbook is designed to automate the deployment of a web application using Ansible. It includes tasks for setting up the server environment, installing necessary packages, deploying the application code, and configuring the web server.

### Testing Connectivity
You can test connectivity to your managed nodes using the `ping` module.
Example command:
```sh
ansible all -m ping
``` 

### Updating Playbook

```sh
---
- hosts: all
  become: yes
  tasks:
    - name: update repository index for Ubuntu
      apt:
        update_cache: yes
      when: ansible_distritution_version == "Ubuntu"
    - name: install apache2 and php packages for Ubuntu
      apt:
        name:
          - apache2
          - libapache2-mod-php
        state: latest
      when: ansible_distritution == "Ubuntu"
    
    - name: update repository index for CentOS
      dnf:
        update_cache: yes
      when: ansible_distritution_version == "CentOS"

    - name: install httpd and php packages for CentOS
      dnf:
        name:
          - httpd
          - php
        state: latest
      when: ansible_distritution == "CentOS"
```

### Playbook with Variables

```sh
---
- hosts: all
  become: yes
  tasks:
    - name: install apache and php
      package:
        name:
          - "{{ web_server_package }}"
          - "{{ php_package }}"
        state: latest
        update_cache: yes
```

