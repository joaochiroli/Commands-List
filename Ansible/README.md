# Ansible

### Ansible sequency

- `ANSIBLE_CONFIG` variable
- ./ansible.cfg
- ~/.ansible.cfg
- /etc/ansible/ansible.cfg

#### Modules => Tasks => Plays => Playbook

### What is ansible.cfg ?
Default configuration file of Ansible; normally, you don't change this file
Example ansible.cfg

```
[defaults]

#--- General settings
interpreter_python      = auto_legacy_silent     --> usado para executar o comando em python em outra máquina independente da versão
forks                   = 5
log_path                = /var/log/ansible.log
module_name             = command
executable              = /bin/bash
ansible_managed         = Ansible managed
host_key_cheking        = false ---> importante para não pedir a chave do host

#--- Files/Directory settings
inventory               = /etc/ansible/hosts
library                 = /usr/share/my_modules
remote_tmp              = ~/.ansible/tmp
local_tmp               = ~/.ansible/tmp
roles_path              = /etc/ansible/roles

#--- Users settings
remote_user             = vagrant
remote_password         = vagrant
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


- `ansible all --list-hosts` list all hosts recognized by ansible
- `ansible ungrouped --list-hosts` list all hosts without group
- `ansible <host-or-group> -i <archive> --list-hosts` list hosts 
- `ansible-inventory -v -i <archive> --graph` list all tree of hosts
- `ansible --version` list the version and the configuration archive
- `ansible-config list` show all config in use
- `ansible-doc -l` list all modules
- `ansible-config`
- `ansible-console`
- `ansible-doc`
- `ansible-galaxy`
- `ansible-inventory`
- `ansible-playbook`
- `ansible-pull`
- `ansible-vault`
- `ansible`



### Ansible Blocks:

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

- **Module** a program (usually python) that executes, does some work and returns proper JSON output. Like: copy, file, yum, service
Example of modules:  
  - Module: `ping` - the simplest module that is useful to verify host connectivity
  - Module: `shell` - a module that executes shell command on a specified host(s)
  - Module: `command` - executes a single command that will not be processed through the shell
  -  `ansible all -m <command>`  like **ansible -m ping all** or **ansible -m shell -a 'date; whoami'**
  -  `ansible all -i setup`  list inventory
  -  `ansible all -m setup` show inventory (ansible facts)
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


### Inventory

Types: **Static Inventory** or  **Dynamic Inventory** 
Parameters: ansible_hosts, ansible_port, etc.

INI
```
[debian]
192.168.15.10

[redhat]
192.168.15.9

[linux:children]
debian
redhat

```

YAML:
```
all:
  children:
    debian:
      hosts:
        192.168.15.8:
    redhat:
      hosts:
        192.168.15.[10:12]:
  vars:
    ansible_user: vagrant --> qual usuário vai se autenticar no host de destino
    ansible_become: yes
    ansible_password: vagrant
```

Command to put extra vars:

```
ansible all --extra-vars guitarra=guitarrista -m debug -a var=guitarra
```

Enable all Plugins and use dinamic groups aws, go to ansible.cfg and put:
```
[inventory]

enable_plugins = aws_ec2, host_list, script, auto, yaml, ini, toml

```

It's possible create a repository call group_vars or host_vars for put files with vars informations 
In host_vars the files need follow this structure: 
<ip>
<hostname>
And inside of file you can put the vars informations

IN group_vars the files need follow this structure:  
<group_name>
And inside this file you put the var informations

### Ansible Collection

- Command = colletion + module
- Colletions Locate /home/joaochiroli/.ansible/collections/ansible_collections/
- Show all collections: ansible-galaxy colletion
- Install collection: ansible-galaxy install grafana.grafana

### Playbook

- ansible-playbook -i <inventary> <playbook> --syntax-check
- ansible-playbook -i <inventary> <playbook> --list-hosts
- ansible-playbook -i <inventary> <playbook> --list-task

#### tags

  You can use tags for set a specific task

```
---
  - name: test
    host: abc
    tasks:
    -   name: Update apt cache
        ansible.builtin.apt:
          update_cache: yes
        tags: debian
...

$ ansible-playbook --tag debian UpdateLinux.yml

```

#### Vars

```
---

- name: testando variáveis
  hosts: debian
  vars: 
    message: "MENSAGEM DE TESTE DA VARIAVEL"
    packages:
      - htop
      - vim  
  tasks: 
    - name: DEBUG
      ansible.builtin.debug:
        msg: "{{ message }}"
    
    - name: Install packages
      ansible.builtin.apt:
        name: "{{ packages }}"
        state: latest 
...

$ ansible-playbook -i hosts playbooks/vars.yml

```

```
---

- name: testando variáveis
  hosts: debian
  vars_files: /etc/ansible/playbook_vars.yml
  vars: 
    message: "MENSAGEM DE TESTE DA VARIAVEL"
    packages:
      - htop
      - vim  
  tasks: 
    - name: DEBUG
      ansible.builtin.debug:
        msg: "{{ message }}"
    
    - name: Install packages
      ansible.builtin.apt:
        name: "{{ packages }}"
        state: latest 
...

file playbook_vars.yml
packages:
  - htop
  - vim
  - tcpdump

$ ansible-playbook -i hosts playbooks/vars.yml

```


```
- name: testando variáveis
  hosts: debian
  tasks: 
    - name: DEBUG | ANSIBLE FACTS
      ansible.builtin.debug:
        msg: "{{ ansible_all_ipv4_addresses }}"

$ ansible -i <inventory> -m setup


```

#### Prompt 

Is possible do a interaction with your playbook


```
---
- name: Ansible Prompt | Creating user on Linux
  hosts: all
  vars_prompt:
    - name: username
      prompt: What is your username?
      private: false
    - name: password
      prompt: What is your password?
      private: true
      encrypt: "md5_crypt"
      confirm: yes
    - name: shell
      prompt: What is your shell ?
      private: false
  tasks:
    - name: Print a message
      ansible.builtin.debug:
        msg: 'Usuario: {{ username }} | Password: {{ password }} | Shell: {{ shell }}'

    - name: USER | Add user
      ansible.builtin.user:
        name: "{{ username }}"
        comment: "User created by Ansible"
        shell: "{{ shell }}"
        home: "/home/{{ username }}"
        password: "{{ password }}"


```

#### Conditions

```
- name: Ansible Conditionals (when)
  hosts: all
  tasks:
    - name: DNF | Update Systems
      ansible.builtin.dnf:
        name: "*"
        state: latest
        update_cache: yes
      when: ansible_distribution == "Rocky"

    - name: APT | Update cache
      ansible.builtin.apt:
        update_cache: yes
      when: ansible_distribution == "Debian"

    - name: APT | Update Systems
      ansible.builtin.apt:
        name: "*"
        state: latest
      when: ansible_distribution == "Debian"
```

#### Conditions - Bool

```
---
- name: Ansible Conditionals
  hosts: rocky01
  vars:
    backup: true
    snapshot: false
  tasks:
    - name: Run the task if 'backup' is true
      ansible.builtin.debug:
        msg: "Congratulations"
      when: backup | bool

    - name: Run the task if 'backup' is false
      ansible.builtin.debug:
        msg: "Critical. Make backup."
      when: not backup

```
#### Blocks
Conjunto de tarefas que voce pode executar, caso uma tarefa nao funcione ele passa pra proxima. 

```
---
- name: Block Testing
  hosts: rocky01
  tasks:
    - block:
        - ansible.builtin.debug:
            msg: "#### EXECUTADO NORMALMENTE ####"
        - name: Simulando erros
          ansible.builtin.shell: ./configure
          args:
            chdir: /tmp
        - ansible.builtin.debug:
            msg: "NUNCA SERA EXECUTADO"
      rescue:
        - ansible.builtin.debug:
            msg: "ERROR - FALHA NO TARGET {{ inventory_hostname }}"
      always:
        - name: SISOP | Update System
          ansible.builtin.dnf:
            name: "*"
            state: latest


```
#### Simple Loop
 

```
---
- name: Ansible Loop
  hosts: rocky01
  tasks:
    - name: USER | Add User
      ansible.builtin.user:
        name: "{{ item }}"
        state: present
        groups: "wheel"
      loop:
        - eddie
        - dime
        - taylor
      loop_control:
        pause: 3    ### voce pode usar um controle entre as instalações

```


#### Compost Loop
 

```
- name: Ansible Loop
  hosts: rocky01
  tasks:
    - name: USER | Add User
      ansible.builtin.user:
        name: "{{ item.name }}"
        state: present
        comment: "{{ item.comment }}"
        groups: "wheel"
      loop:
        - { name: 'eddie', comment: 'Van Halen' }
        - { name: 'dime', comment: 'Pantera' }
        - { name: 'taylor', comment: 'Foo Fighters' }

```

or

```
- name: Ansible Loop
  hosts: rocky01
  tasks:
    - name: SYSTEM | Copy files
      ansible.builtin.copy: 
        src: "{{ item.src }}" 
        dest: "{{ item.dest }}"
      with_items:
        - { src: '/tmp/file1.txt', dest: '/tmp/file1.txt' }
        - { src: '/tmp/file2.txt', dest: '/tmp/file2.txt' }
        - { src: '/tmp/file3.txt', dest: '/tmp/file3.txt' }
```

#### Handles
 

```

- name: Ansible Handlers
  hosts: rocky01
  tasks:
    - name: NGINX | Change Listener
      ansible.builtin.replace:
        dest: /etc/nginx/nginx.conf
        regexp: 'listen       80 default_server;'
        replace: 'listen       {{ ansible_default_ipv4.address }}:80 default_server;'


```


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

