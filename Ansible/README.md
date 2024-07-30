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

### What is ansible.cfg ?
  Default configuration file of Ansible; normally, you don't change this file