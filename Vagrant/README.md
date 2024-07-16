# Inicializando a VM
- `vagrant init`           -- Inicialize o Vagrant com um diretório Vagrantfile e ./.vagrant, sem usar nenhuma imagem base especificada. Antes de poder fazer o vagrant up, você precisará especificar uma imagem base no Vagrantfile.
- `vagrant init <boxpath>` -- Inicialize o Vagrant com uma caixa específica. Para encontrar uma caixa, acesse o [catálogo público de caixas do Vagrant](https://app.vagrantup.com/boxes/search). Quando você encontrar um que goste, basta substituir seu nome por boxpath. Por exemplo, `vagrant init ubuntu/trusty64`.


# Iniciar a VM
- `vagrant up`                  -- inicia ambiente vagabundo (também disposições apenas no PRIMEIRO vagabundo)
- `vagrant resume`              -- retomar uma máquina suspensa (vagrant up também funciona bem para isso)
- `vagrant provision`           -- força o reprovisionamento da máquina vagabunda
- `vagrant reload`              -- reinicia a máquina vagrant, carrega a nova configuração do Vagrantfile
- `vagrant reload --provision`  -- reinicie a máquina virtual e force o provisionamento

# Dicas
- `vagrant -v`                    -- vagrant version
- `vagrant status`                -- status da máquina
- `vagrant global-status`         -- status de todas as máquinas
- `vagrant global-status --prune` -- igual ao anterior, mas remove entradas inválidas
- `vagrant provision --debug`     -- use o sinalizador de depuração para aumentar o detalhamento da saída
- `vagrant push`                  -- sim, o vagrant pode ser configurado para [deploy code](http://docs.vagrantup.com/v2/push/index.html)!
- `vagrant up --provision | tee provision.log`  -- Runs `vagrant up`, força o provisionamento e registra todas as saídas em um arquivo

# Entrando em uma VM 
- `vagrant ssh`           -- connectando via SSH
- `vagrant ssh <boxname>` -- Se você der um nome à sua caixa no Vagrantfile, poderá fazer ssh nela com boxname. Funciona em qualquer diretório.

# Parando a VM
- `vagrant halt`        -- stops a vm
- `vagrant suspend`     -- suspends a vm (lembra do estado)

# Deletando a VM
- `vagrant destroy`     -- para e apaga todos os vestígios da máquina vagabunda
- `vagrant destroy -f`   -- igual ao anterior, sem confirmação

# Boxes
- `vagrant box list`              -- veja uma lista de todas as caixas instaladas no seu computador
- `vagrant box add <name> <url>`  -- download de um box image no seu computador
- `vagrant box outdated`          -- verifique se há atualizações atualização da caixa vagrant
- `vagrant box remove <name>`   -- exclui uma caixa da máquina
- `vagrant package`               -- empacota um ambiente de caixa virtual em execução em uma caixa reutilizável

# Salvando Progresso
- `vagrant snapshot save [options] [vm-name] <name>` -- vm-name geralmente é `default`. Permite-nos salvar para que possamos reverter mais tarde

# Plugins
- [vagrant-hostsupdater](https://github.com/cogitatio/vagrant-hostsupdater) : `$ vagrant plugin install vagrant-hostsupdater` to update your `/etc/hosts` arquivo automaticamente cada vez que você inicia/para sua caixa vagrant.

# Notas
- Se vocês estão usando [VVV](https://github.com/varying-vagrant-vagrants/vvv/),você pode ativar o xdebug executando `vagrant ssh` e então `xdebug_on` da CLI da máquina virtual.

# Config Vagrantfile Exemplo 1 

    Vagrant.configure('2') do |config|
      config.vm.define "vm1" do |vm1|
        vm1.vm.box = "ubuntu/bionic64"
        vm1.vm.hostname = "vm1"
        vm1.vm.network "public_network", ip: "192.168.33.10"
      end

      config.vm.define "vm2" do |vm2|
        vm2.vm.box = "ubuntu/bionic64"
        vm2.vm.hostname = "vm2"
        vm2.vm.network "public_network", ip: "192.168.33.11"
      end
      
       config.vm.define "vm3" do |vm3|
        vm3.vm.box = "ubuntu/bionic64"
        vm3.vm.hostname = "vm3"
        vm3.vm.network "public_network", ip: "192.168.33.12"
       end
    end

# Config Vagrantfile Exemplo 2 

    Vagrant.configure("2") do |config|
      config.vm.define "vm1" do |vm1|
        vm1.vm.box = "ubuntu/trusty64"
        $$vm1.vm.network "private_network", ip: "192.168.15.8"
        vm1.vm.network "public_network", bridge: "wlp3s0", ip: "192.168.15.8"
      vm1.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
        vb.name = "vm1"
      end
      vm1.vm.provision "shell", inline: <<-SHELL
        apt-get update
        apt-get install -y apache2
      SHELL
      end
    end

# Config Vagrantfile Loop

    Vagrant.configure("2") do |config|
      (1..2).each do |i|
          config.vm.define "web_#{i}" do |web|
              web.vm.box = "centos/7"
              web.vm.network "public_network", bridge: "enp8s0", ip: "192.168.0.12#{i}"
              web.vm.provision "shell", path: "httpd_#{i}.sh"
          end
      end
  
      (1..2).each do |i|
         config.vm.define "lb_ipvsadm_#{i}" do |lb_ipvsadm|
             lb_ipvsadm.vm.box = "centos/7"
             lb_ipvsadm.vm.network "public_network", bridge: "enp8s0", ip: "192.168.0.12#{i+2}"
             lb_ipvsadm.vm.provision "shell", inline: <<-SHELL
              apt-get update
              apt-get install -y apache2
             SHELL
         end
      end
     end
