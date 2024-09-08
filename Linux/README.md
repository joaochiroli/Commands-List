# Linux
##### Comandos básicos

- `ls`
- `ls -l`
- `ls -la `
- `cd`
- `pwd`
- `mkdir`
- `rm`
- `rm -rf`
- `cp <file1> <file2>`
- `mv <file1> <file2>`
- `touch file`
- `cat file`
- `cat > file`
- `tail -f`
- `tail -n`
- `grep`
- `locate file`
- `whereis app` show possible locations of app
- `top`
- `ps -aux`
- `find [path] [expression]` like find /etc -name "nginx"
- `echo -n "Qual sua idade ?"`  faz com que a pergunta seja exibida na mesma linha
- `wc -w` conta a quantidade de palavras em um arquivo


##### Comandos básicos Network

- `ping host` ping host
- `whois domain` get whois for domain
- `dig domain` get DNS for domain
- `dig -x host` reserve lookup host
- `wget file` download file
- `wget -c file` continue stopped download
- `wget -r url` recursively download files from url
- `curl url` outputs the webpage from url
- `curl -o mehhtml url` writes the page to mehhtml
- `ssh user@host` 
- `ssh -p port user@host` 
- `ssh -D user@host` connect & use bind port
- `ipconfig`
- `ip addr`
- `route`
- `netstat`
- `tcpdump`
- `ping`
- `traceroute`
- `nslookup`
- `netstat -a`

files:
- /etc/resolv.conf
- /etc/hostname
- /etc/ssh/sshd_config
- /etc/hosts


##### Permissões

- 4 - read (r)
- 2 - write (w)
- 1 - execute (x)

- order: owner(user)/group/other

- chmod 777 - rwx ever
- chmod 755 - rw for owner, for group world

##### Variáveis

- SHELL=/bin/bash
- HOME=/home/USER
- USER=chiroli

- KEY=value

##### TAR

tar

    tar -cvf techplayon.tar techplayon (compressing)
    tar -xvf techplayon.tar (uncompressing)

gzip

    tar -czvf techplayon.tar.gz techplayon (compressing)
    tar -xzvf techplayon.tar.gz (uncompressing)

# Script

##### variáveis
- nome="João"
- idade=25

```
echo $HOME

output
/root

```

- function saudacao() {
    echo "Olá, terráqueo $1!"
}

```
input 
saudacao chiroli

output
Olá, terráqueo chiroli!

```

- argumentos 
    - `$0:` Contém o nome do próprio script
    - `$1 $2, $3,...` Contêm os valores dos argumentos passados na ordem em que foram fornecidos.
    - `$@:` Contém todos os argumentos passados, separados por espaço.
    - `$*:` Contém todos os argumentos passados como uma única string, separados por espaço.
    - `$#:` Contém o número total de argumentos passados.


- condicional 

```
if [ condição ]; then 
    # bloco de código a ser executado se a condição for verdadeira
else
    # bloco de código a ser executado se a condição for falsa
fi
```

- variavel exemplo:
```
### user input um valor pra repo_value ###
read repo_value

### repo output ###
echo "Adding the Kubernetes repository with the value: $repo_value"


```

- Loops 
    - while:
    ```
    while [ "$input" != "exit" ]
    do
        echo "Type something (type 'exit' to quit):"
        read input
        echo "You typed: $input"
    done
    ```
    - for:
    ```
    for number in 1 2 3 4 5
    do
        echo "Number: $number"
    done

    ```

- **EXEMPLO PRÁTICO**
```
IFS=:   ### Aqui, ele está sendo definido como :. Isso significa que o script irá usar o caractere : como delimitador para separar os campos em cada linha que ele ler.
while read -r usuario senha uid gid nome_completo home shell; do
  echo "Usuário: $usuario"
  echo "UID: $uid"
  echo "GID: $gid"
  echo "Diretório Home: $home"
  echo "Shell padrão: $shell"
  echo ""
done < /etc/passwd ## Esta linha indica o fim do loop while e direciona a entrada (< /etc/passwd) para o arquivo /etc/passwd. Isso significa que o loop while continuará processando cada linha desse arquivo até que todas as linhas tenham sido lidas e processadas.
```

Se quiser fazer somas com variáveis
```
$(($idade +5))
```
colocando o parametro -s nao mostra voce digitando a senha por exemplo
```
read -s senha
read -p "Enter the resource group name: " rg_name
```

- **EXEMPLO PRÁTICO**
```
echo "Digite algumas frutas (digite 'fim' para sair:)"
while read fruta 
do
  if [ "$fruta" == "fim" ]
  then
    break
  fi
  echo "Você digitou: $fruta"
done

```
```
d (){
  git add .
  git commit -m "commit automático"
  git push -u origin main
}

```
