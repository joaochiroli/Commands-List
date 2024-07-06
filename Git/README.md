# Install Vagrant

    sudo su
    apt-get update && apt-get install -y libvirt-dev ruby-all-dev apparmor-utils
    curl -O -L https://dl.bintray.com/mitchellh/vagrant/vagrant_1.6.5_x86_64.deb
    dpkg -i vagrant_1.6.5_x86_64.deb 
    aa-complain /usr/lib/libvirt/virt-aa-helper # workaround
    exit

## Install vagrant-kvm as user

    vagrant plugin install vagrant-kvm 

