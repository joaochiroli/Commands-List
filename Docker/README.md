
#### Gerenciamento de Containers
- docker ps: Lista os containers em execução.
- docker ps -a: Lista todos os containers, incluindo os que estão parados.
- docker start [container]: Inicia um container que está parado.
- docker stop [container]: Para um container em execução.
- docker restart [container]: Reinicia um container.
- docker rm [container]: Remove um container.
- docker logs [container]: Exibe os logs de um container.
- docker exec -it [container] [command]: Executa um comando dentro de um container em execução (ex.: abrir um terminal bash).
- docker exec -it mdc-container bash

#### Imagens
- docker images: Lista todas as imagens disponíveis localmente.
- docker pull [image]: Baixa uma imagem do Docker Hub ou de um repositório.
- docker rmi [image]: Remove uma imagem local.
- docker build -t [tag] .: Constrói uma imagem a partir de um Dockerfile no diretório atual.
- docker tag [image_id] [repository:tag]: Marca uma imagem com uma nova tag.

#### Volumes e Rede
- docker volume create [volume_name]: Cria um volume.
- docker volume ls: Lista volumes criados.
- docker network create [network_name]: Cria uma rede Docker.
- docker network ls: Lista redes Docker criadas.
- docker network connect [network_name] [container_name]: Conecta um container a uma rede específica.
- docker run -d -v $(pwd)/mdc-volume:/data --name mdc-container ubuntu tail -f /dev/null - create a container and mount the volume


#### Gerenciamento de Imagens e Containers
- docker run [options] [image]: Cria e inicia um novo container a partir de uma imagem.

#### Opções úteis:
- -d: Executa o container em segundo plano (modo detached).
- -p [host_port]:[container_port]: Mapeia a porta do container para a máquina host.
- --name [container_name]: Dá um nome ao container.
- -v [host_dir]:[container_dir]: Mapeia um volume do host para o container.
- --rm: Remove o container após ele ser parado.
docker inspect [container/image]: Exibe informações detalhadas sobre o container ou imagem.

#### Manutenção
- docker system prune: Remove containers, volumes e imagens não utilizados para liberar espaço.
- docker stats: Exibe o uso de recursos (CPU, memória, etc.) de containers em execução.

Multi stage build usado em liguagens de programação compilada como Go
