# Ansible

### Ansible sequency

- `ANSIBLE_CONFIG` variable
- ./ansible.cfg
- ~/.ansible.cfg
- /etc/ansible/ansible.cfg

### What is ansible.cfg ?
Default configuration file of Ansible; normally, you don't change this file
Example ansible.cfg

```
[defaults]

#--- General settings
forks                   = 5
log_path                = /var/log/ansible.log
module_name             = command
executable              = /bin/bash
ansible_managed         = Ansible managed

#--- Files/Directory settings
inventory               = /etc/ansible/hosts
library                 = /usr/share/my_modules
remote_tmp              = ~/.ansible/tmp
local_tmp               = ~/.ansible/tmp
roles_path              = /etc/ansible/roles

#--- Users settings
remote_user             = root
sudo_user               = root
ask_pass                = no
ask-sudo_pass           = no

#--- SSH settings
remote_port             = 22
timeout                 = 10
host_key_checking       = False
ssh_executable          = /usr/bin/ssh
private_key_file        = ~/.ssh/id_rsa

[privilege_scalation]

become                  = True
become_method           = sudo
become_user             = root
become_ask_pass         = False

[ssh_connection]

scp_if_ssh              = smart
transfer_method         = smart
retries                 = 3

```

### Commands 

```
$ ansible all --list-hosts` list all hosts recognized by ansible

$ ansible ungrouped --list-hosts` list all hosts without group

$ ansible <host-or-group> -i <archive> --list-hosts` list hosts 

$ ansible-inventory -v -i <archive> --graph` list all tree of hosts 

$ ansible --version` list the version and the configuration archive

$ ansible-config list` show all modules in use 

$ ansible-doc list` show all modules in use 
```

### Modules => Tasks => Plays => Playbook.

Let us see buidlding blocks about Ansible:

- **Inventory:** It is a simple list of hosts; /etc/ansible/hosts
- **Playbook or commands:** Execution of desired actions.
- **API:** Cloud Services
- **SSH, WinRM:** Work via transport layer.
- **Ansible roles:** Special kind of playbook that are fully self-contained with tasks, variables, configurations templates and other supporting files.
- **Ansible Galaxy:** Like git repo,collection of playbooks available as open source.
- **Ansible Tower:** Ansible Tower is a web-based interface for managing Ansible.
- **Ansible AWX:** It is the open source version of Ansible Tower & a web-based solution that makes Ansible even more easy to use for IT teams of all kinds. It’s designed to be the hub for all of your automation tasks. Simple, Powerful and agentless (unlike Puppet).

### Module

- **AD HOC** command-line tool to automate a single task on one or more managed nodes.

- **Module** a program (usually python) that executes, does some work and returns proper JSON output
Example of modules:  
  - Module: `ping` - the simplest module that is useful to verify host connectivity
  - Module: `shell` - a module that executes shell command on a specified host(s)

  ```
  $ ansible -m ping all
  $ ansible -m shell -a 'date; whoami' localhost #hostname_or_a_group_name

  ```
  - Module: `command` - executes a single command that will not be processed through the shell
  -  `ansible all -m <command>`  
  -  `ansible all -m setup`  list inventory
  -  `ansible all -m setup` show inventory 
  -  `ansible all -m setup -a "filter=ansible_default_ipv4"` show inventory and a specific information 
  -  `ansible all -m copy -a "src=./ansible.cfg dest=/tmp mode=644 owner=vagrant"` copy localhost to guest
  -  `ansible-config list -t <module>` show especific module in use like **ansible-config list -t become**
  - `ansible-config init > ansible.cfg` sent a new ansible file with all configurations
  - `-k` ask the password 
  - `-b` elevate privilegies
  - `-K` ask the password to elevate privilegies
  - `-v` verbose
  - `ansible all -m shell -a "/sbin/reboot" -b` reboot vms
  - `ansible all -m systemd -a "name=sshd state=restarted" -b` restart services



  










### SSH configuration 

```
########## Create Key ###############

ssh-keygen -b 2048 -t rsa

########## Sent the Key #############

ssh-copy-id -i id_rsa.pub vagrant@192.168.15.8


```

```
######## Environment Variable Configuration ######## 

export ANSIBLE_CONFIG=/tmp/ansible.cfg
echo $ANSIBLE_CONFIG

```

