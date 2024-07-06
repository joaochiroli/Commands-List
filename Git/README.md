# A primeira coisa que você deve fazer ao instalar Git é configurar seu nome de usuário e endereço de e-mail. Isto é importante porque cada commit usa esta informação, e ela é carimbada de forma imutável nos commits que você começa a criar:
    git config --global user.name "Fulano de Tal"
    git config --global user.email fulanodetal@exemplo.br 

# Install Vagrant

    sudo su
    apt-get update && apt-get install -y libvirt-dev ruby-all-dev apparmor-utils
    curl -O -L https://dl.bintray.com/mitchellh/vagrant/vagrant_1.6.5_x86_64.deb
    dpkg -i vagrant_1.6.5_x86_64.deb 
    aa-complain /usr/lib/libvirt/virt-aa-helper # workaround
    exit

## Install vagrant-kvm as user

    vagrant plugin install vagrant-kvm 

