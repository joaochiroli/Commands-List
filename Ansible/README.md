# Ansible


- `grupos aninhados` groups by groups 

```
[start:end]

[usa]
www.casa[1:2].example.com
192.168.88.[0:255]
```

```
sudo vim /etc/ansible/hosts

### HOST OUTSIDE GROUP ###

192.168.88.4 

### HOST INSIDE THE GROUP ###

[webservers]
serverb.lab.example.com
```
`ansible all --list-hosts` list all hosts recognized by ansible

`ansible ungrouped --list-hosts` list all hosts without group

`ansible <host-or-group> -i <archive> --list-hosts` list hosts 

`ansible all -i <archive> --list-hosts` list all hosts 

`ansible-inventory -v -i <archive> --graph` list all tree of hosts 

`ansible --version` list the version and the configuration archive

`ansible --version` list the version and the configuration archive

`ansible all -m ping` ping all hosts

### What is ansible.cfg ?
  Default configuration file of Ansible; normally, you don't change this file

### Ansible sequency

- `ANSIBLE_CONFIG` variable
- ./ansible.cfg
- ~/.ansible.cfg
- /etc/ansible/ansible.cfg

```
[defaults]
inventory = ./inventory
remote_user = UsuarioNoHostGerenciado
ask_pass = true
host_key_checking = false

[privilege escalation]
become = true
become_method = sudo
become_user = root
become_ask_pass = true

```