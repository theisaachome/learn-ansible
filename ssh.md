## SSH Overview and Setup

SSH (Secure Shell) is a cryptographic network protocol used for secure communication between two systems over an unsecured network. It is commonly used for remote login and command execution on servers.


### Prequisites
Before setting up SSH for Ansible, ensure the following prerequisites are met:
- Ensure that SSH is installed on both the control node and the managed nodes.
- Ensure that you have network connectivity between the control node and the managed nodes.
- Ensure that you have the necessary permissions to access the managed nodes via SSH.

### Setting up SSH connections
Connect to each server from the control node using SSH to ensure that the connection is working. 
For example:
```sh
$ ssh user@managed_node_ip  
$ ssh ivel@172.16.250.133 

note: for initial connection "yes" may be required to add the host to known_hosts file.
```

### Generating SSH Keys
To set up SSH key-based authentication, you need to generate a pair of SSH keys (a private key and a public key) on your local machine.
You can generate SSH keys using the following command:
```sh
ssh-keygen -t rsa -b 4096 -C "example default"
```
or
```sh
ssh-keygen -t ed25519 -C "ivel default"
```
### Copying SSH Public Key to Managed Nodes
Once you have generated the SSH keys, you need to copy the public key to each managed node to enable passwordless SSH login.
You can use the `ssh-copy-id` command to copy the public key to the managed nodes:
```sh
ssh-copy-id (source) (target-server)
```
Example:
```sh
ssh-copy-id ~/.ssh/id_rsa.pub ivel@172.16.250.13

```

### Generating a Specific Key for Ansible (Over Controller Node)
It is a good practice to create a specific SSH key pair for Ansible to use, rather than using your default SSH keys.
You can generate a new SSH key pair specifically for Ansible using the following command:
```sh
ssh-keygen -t ed25519   -C "ansible-key" -f ~/.ssh/ansible
``` 
### Copying Ansible SSH Key to Managed Nodes
After generating the Ansible-specific SSH key pair, copy the public key to each managed node using the `ssh-copy-id` command:
```sh
ssh-copy-id -i ~/.ssh/ansible.pub ivel@172.16.250
```

### Example 

We have 4 servers with One as the control node and three as managed nodes.
