# Project Overview

## Objetivo

Subir um ambiente de monitoramento usando Zabbix em 3 camadas (Zabbix Server, DB e Web), integrar com o Grafana, usar API do Zabbix para adicionar hosts, integrar com o GLPI para abertura de ticket, utilizando Vagrant para automatizar e criação das vms.

## Tecnologias Envolvidas

1. **Vagrant**
2. **Linux**
3. **Zabbix**
4. **Grafana**
5. **API**
6. **PostgreSQL**
7. **Nginx**  
8. **GLPI** 



# Subir as VMS

1. Primeira coisa a se fazer é subir o Vagrant usando o arquivo Vagrantfile e seus scripts para subir as vms que serão utilizadas


        vagrant up 
    

# Conectar a VM DB e configurar PostgreSQL

1. Conectar a VM e começar a configurar o DB

        vagrant ssh vm2
        export LANGUAGE=en_US.UTF-8
        export LANG=en_US.UTF-8
        export LC_ALL=en_US.UTF-8

2. Instalando DB PostgreSQL  
    
        apt-cache madison postgresql
        sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
        curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gp
        sudo apt install postgresql-16 postgresql-contrib-16
        sudo systemctl enable postgresql.service
        sudo systemctl start postgresql.servic


3. Criando usuário e Base de Dados

        sudo -u postgres createuser --pwprompt zabbix
        sudo -u postgres createdb -O zabbix -E Unicode -T template0 zabbix


4. Liberações de Network para acesso a DB 

        vi /etc/postgresql/16/main/pg_hba.conf  
            host    all             all             0.0.0.0/0               md5
            host    all             all             ::1/128                 md5
        vi /etc/postgresql/16/main/postgresql.conf
            listen_addresses = '*'


5. Caso queira acessar o Banco e realizar alguns comandos (Opcional)

        Acesse o prompt do PostgreSQL como o usuário postgres
            sudo -u postgres psql
        Dentro do prompt do PostgreSQL, conecte-se ao banco de dados zabbix
            \c zabbix
        Listar todas as tabelas do banco de dados zabbix
            \dt    
        Listar todas os usuarios do banco de dados zabbix
            \du


6. Comandos finais dessa etapa

        systemctl restart postgresql
        apt install zabbix-agent -y
        systemctl start zabbix-agent 
        systemctl enable zabbix-agent 



# Conectar a VM Zabbix Server e começar a configurar

1. Conectar a VM e começar a configurar o Zabbix Server


        vagrant ssh vm1
        sudo su
        apt-get update
        export LANGUAGE=en_US.UTF-8
        export LANG=en_US.UTF-8
        export LC_ALL=en_US.UTF-8
        wget https://repo.zabbix.com/zabbix/7.0/debian/pool/main/z/zabbix-release/zabbix-release_7.0-2+debian12_all.deb
        apt update
        dpkg -i zabbix-release_7.0-2+debian12_all.deb


2. Instalando ferramenta client do DB para testar conexão remota 


        sudo apt-get install postgresql-client
        psql -h 192.168.15.9 -U zabbix_server -d zabbix -W


3. Instalando pacotes do Zabbix Server e pacotes das tabelas do DB


        apt install zabbix-server-pgsql zabbix-sql-scripts zabbix-agent


4. Preenchendo a Base de Dados com as tabelas do Zabbix Server


        zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | psql -h 192.168.15.9 -U zabbix -d zabbix


5. Preenchendo a Base de Dados com as tabelas do Zabbix Server


        vi /etc/zabbix/zabbix_server.conf
            DBPassword=password
            DBHost=<ip do host que ta o db>


6. Comandos finais


        systemctl start zabbix-server   
        systemctl enable zabbix-server
        apt install zabbix-agent -y
        systemctl start zabbix-agent 
        systemctl enable zabbix-agent



# Conectar a VM WEB e começar a configurar

1. Conectar a VM e começar a configurar o servidor Web


        vagrant ssh m3
        sudo su
        apt-get update
        apt install 
        export LANGUAGE=en_US.UTF-8
        export LANG=en_US.UTF-8
        export LC_ALL=en_US.UTF-8


2. Instalando binários do Zabbix para utilizar a parte WEB


        wget https://repo.zabbix.com/zabbix/7.0/debian/pool/main/z/zabbix-release/zabbix-release_7.0-2+debian12_all.deb
        apt update
        dpkg -i zabbix-release_7.0-2+debian12_all.deb
        apt install zabbix-frontend-php php8.2-pgsql zabbix-nginx-conf
        vi etc/zabbix/nginx.conf
            # listen 80;
            # server_name 192.168.15.10; 
        vi /etc/php/8.2/fpm/php.ini
            date.timezone = America/Sao_Paulo
    
3. Comandos finais


        systemctl start nginx php8.2-fpm
        systemctl enable nginx php8.2-fpm
        apt install zabbix-agent -y
        systemctl start zabbix-agent 
        systemctl enable zabbix-agent



# Conectar ao Zabbix Server

1. Parar serviço do Zabbix Server

    
        systemctl stop zabbix-server
   

# Conectar ao DB para habilitar o Timescaledb


1. Instalar binários do Timescaledb


        echo "deb https://packagecloud.io/timescale/timescaledb/debian/ $(lsb_release -c -s) main" | sudo tee /etc/apt/sources.list.d/timescaledb.list
        wget --quiet -O - https://packagecloud.io/timescale/timescaledb/gpgkey | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/timescaledb.gpg
        sudo apt update
        sudo apt install timescaledb-2-postgresql-16=2.13.1~debian12 timescaledb-2-loader-postgresql-16=2.13.1~debian12
        sudo timescaledb-tune
        sudo systemctl restart postgresql


2. Criando extensão 


        echo "CREATE EXTENSION IF NOT EXISTS timescaledb CASCADE;" | sudo -u postgres psql zabbix


3. Editando configurações 


        vi /etc/postgresql/16/main/postgresql.conf
            max_connections = 200
            superuser_reserved_connections = 10
        sudo systemctl restart postgresql
    


# Conectar ao Zabbix Server


1. Populando Timescaledb e dando start no Zabbix Server 


        cat /usr/share/zabbix-sql-scripts/postgresql/timescaledb/schema.sql | psql -h 192.168.15.9 -U zabbix -d zabbix
        systemctl start zabbi-server



# GRAFANA 

    
1. Instalando pacotes



        sudo apt-get install -y apt-transport-https software-properties-common wget
        sudo mkdir -p /etc/apt/keyrings/
        wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
        echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
    
2. Iniciando programas    


        sudo apt-get update
        sudo apt-get install grafana
        systemctl enable grafana-server
        systemctl start grafana-server
        apt install zabbix-agent -y
        systemctl start zabbix-agent 
        systemctl enable zabbix-agent


3. Conectando na página Web 


        Ir até a http://192.168.15.11:3000/ logar com user admin e senha admin 
        Ir até a aba Plugins, instalar e habilitar plugin Zabbix 



# Editar o arquivo de Configuração de todos os Zabbix Agents de todas as vms


1. Editando o arquivo de configuração do Zabbix Server e iniciando o arquivo 

        vi /etc/zabbix/zabbix_agentd.conf
            Server=<ipdozabbixserver>
            apagar parametros Hostname e ServerActive
        systemctl restart zabbix-agent



# Usando Integração com API e Postman para criar hosts 

1. Usar o comando abaixo para retornar o token de autenticação 


        {
            "jsonrpc": "2.0",
            "method": "host.get",
            "params": {
                "output": "extend"
            },
            "auth": "09908de562e8c5231fda8999cc1ab2c3",
            "id": 1
        }



2. Usar o comando abaixo para saber qual o ID do template que iremos utilizar 


        {
            "jsonrpc": "2.0",
            "method": "template.get",
            "params": {
                "output": ["name","templateid"]
            },
            "auth": "09908de562e8c5231fda8999cc1ab2c3",
            "id": 1
        }


3. Usar o comando abaixo para saber qual o ID do grupo que iremos utilizar  


        {
            "jsonrpc": "2.0",
            "method": "hostgroup.get",
            "params": {
                "output": ["name","groupid"]
            },
            "auth": "6eb64c4af84e022c162b3194c10cb052",
            "id": 1
        }       

4. Criar host completo

        {
            "jsonrpc": "2.0",
            "method": "host.create",
            "params": {
                "host": "Grafana",
                "groups": [
                    {
                        "groupid": "2"
                    }
                ],
                "interfaces": [
                    {
                        "type": "1",
                        "main": "1",
                        "useip": "1",
                        "ip": "192.168.15.9",
                        "dns": "",
                        "port": "10050"
                    }
                ],
                "templates": [
                    {
                        "templateid": "10001"
                    }
                ]
            },
            "auth": "2940c2d542bfb846a6083a4779e93941",
            "id": 1
        }



# Integrando Grafana e Zabbix 


1. Integrando as ferramentas


        Criar um user no Zabbix com permissão para integrar com o Grafana
        Colocar as informações de URL, user e password
            http://192.168.15.10/api_jsonrpc.php




# GLPI

1. Instalando pacotes


        sudo apt update
        sudo apt install -y apache2 mariadb-server php php-mysql libapache2-mod-php php-gd php-ldap php-xml php-mbstring php-curl php-json php-intl


2. Configurando DB


        sudo mysql -u root -p
        CREATE DATABASE glpidb CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
        CREATE USER 'glpiuser'@'localhost' IDENTIFIED BY 'password';
        GRANT ALL PRIVILEGES ON glpidb.* TO 'glpiuser'@'localhost';
        FLUSH PRIVILEGES;
        EXIT;

3. Instalando binários e dando permissões as pastas

        wget https://github.com/glpi-project/glpi/releases/download/10.0.16/glpi-10.0.16.tgz
        tar -xzf glpi-10.0.16.tgz
        sudo mv glpi /var/www/html/
        sudo chown -R www-data:www-data /var/www/html/glpi
        sudo chmod -R 755 /var/www/html/glpi


4. Configurações Web

        sudo nano /etc/apache2/sites-available/glpi.conf

        <VirtualHost *:80>
                ServerAdmin admin@example.com
                DocumentRoot /var/www/html/glpi
                ServerName example.com

                ErrorLog ${APACHE_LOG_DIR}/error.log
                CustomLog ${APACHE_LOG_DIR}/access.log combined

                <Directory /var/www/html/glpi>
                    Options FollowSymLinks
                    AllowOverride All
                    Require all granted
                </Directory>
        </VirtualHost>


5. Configurando serviços 



        sudo a2ensite glpi.conf
        sudo systemctl restart apache2



6. Configurações Finais


        Para integrar com o Zabbix precisar criar o token para o usuario glpi
        Ir em configurações geral e habilitar api e atutenticação 
        Criar usuário

