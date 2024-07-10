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
- `vagrant ssh`           -- connects to machine via SSH
- `vagrant ssh <boxname>` -- If you give your box a name in your Vagrantfile, you can ssh into it with boxname. Works from any directory.

# Parando a VM
- `vagrant halt`        -- stops the vagrant machine
- `vagrant suspend`     -- suspends a virtual machine (remembers state)

# Cleaning Up a VM
- `vagrant destroy`     -- stops and deletes all traces of the vagrant machine
- `vagrant destroy -f`   -- same as above, without confirmation

# Boxes
- `vagrant box list`              -- see a list of all installed boxes on your computer
- `vagrant box add <name> <url>`  -- download a box image to your computer
- `vagrant box outdated`          -- check for updates vagrant box update
- `vagrant box remove <name>`   -- deletes a box from the machine
- `vagrant package`               -- packages a running virtualbox env in a reusable box

# Salvando Progresso
-`vagrant snapshot save [options] [vm-name] <name>` -- vm-name is often `default`. Allows us to save so that we can rollback at a later time

# Plugins
- [vagrant-hostsupdater](https://github.com/cogitatio/vagrant-hostsupdater) : `$ vagrant plugin install vagrant-hostsupdater` to update your `/etc/hosts` file automatically each time you start/stop your vagrant box.

# Notas
- If you are using [VVV](https://github.com/varying-vagrant-vagrants/vvv/), you can enable xdebug by running `vagrant ssh` and then `xdebug_on` from the virtual machine's CLI.
