
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

Exemplo de Docker Compose:

´´´
version: '3'
services:
  mysql-mdc:
    image: mysql:latest
    container_name: mysql-mdc
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: mdc_db
      MYSQL_USER: mdc_user
      MYSQL_PASSWORD: mdc_password
    networks:
      - mdc-network

  tshoot-mdc:
    build:
      context: ./mdc-tshoot/
      dockerfile: Dockerfile
    container_name: tshoot-mdc
    restart: always
    networks:
      - mdc-network

networks:
  mdc-network:
    driver: bridge

´´´

- ´docker-compose up -d´ para executar o docker compose

Exemplo de container de troubleshooting

´´´
# Usando a imagem base do Ubuntu 20.04
FROM ubuntu:20.04

# Definindo o diretório de trabalho dentro do contêiner
WORKDIR /app

# Atualizando o sistema operacional dentro do contêiner
RUN apt-get update

# Instalando pacotes necessários (exemplo: curl e vim)
RUN apt-get install -y curl vim telnet mysql-client iputils-ping

# Expondo a porta 80 para acessar a aplicação web
EXPOSE 8080

# Definindo o comando de inicialização do contêiner (exemplo: executando o Apache HTTP Server)
CMD ["sh", "-c", "while true; do sleep 1; done"]

´´´

Exemplo de container Go

´´´
# Imagem base
FROM golang:latest

# Diretório de trabalho
WORKDIR /app

# Copiar os arquivos para o diretório de trabalho
COPY . .

# Compilar o código
RUN go build -o main .

# Comando de execução
CMD ["./main"]

´´´

Exemplo de container Go multi stage

´´´
# Primeira etapa: compilação do código
FROM golang:latest AS build

WORKDIR /app

# Copiar os arquivos necessários
COPY . .

# Compilar o código
RUN go mod download
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .

# Segunda etapa: imagem final mínima
FROM alpine:latest

WORKDIR /app

# Copiar o binário compilado da etapa anterior
COPY --from=build /app/main .

# Comando de execução
CMD ["./main"]
´´´
