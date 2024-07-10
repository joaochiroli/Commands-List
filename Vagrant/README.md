# Inicializando a VM
- `vagrant init`           -- Inicialize o Vagrant com um diretório Vagrantfile e ./.vagrant, sem usar nenhuma imagem base especificada. Antes de poder fazer o vagrant up, você precisará especificar uma imagem base no Vagrantfile.
- `vagrant init <boxpath>` -- Inicialize o Vagrant com uma caixa específica. Para encontrar uma caixa, acesse o [catálogo público de caixas do Vagrant](https://app.vagrantup.com/boxes/search). Quando você encontrar um que goste, basta substituir seu nome por boxpath. Por exemplo, `vagrant init ubuntu/trusty64`.


# Iniciar a VM
- `vagrant up`                  -- inicia ambiente vagabundo (também disposições apenas no PRIMEIRO vagabundo)
- `vagrant resume`              -- retomar uma máquina suspensa (vagrant up também funciona bem para isso)
- `vagrant provision`           -- força o reprovisionamento da máquina vagabunda
- `vagrant reload`              -- reinicia a máquina vagrant, carrega a nova configuração do Vagrantfile
- `vagrant reload --provision`  -- reinicie a máquina virtual e force o provisionamento
