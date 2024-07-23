#### Baseado no Repo: https://github.com/bregman-arie/devops-exercises/blob/master/topics/git/README.md

#### Youtube: https://www.youtube.com/watch?v=oc9bRgUV7hE

## Exercicios

| Name              | Topic  | Objective & Instructions         | Solution                                    | Comments |
| ----------------- | ------ | -------------------------------- | ------------------------------------------- | -------- |
| My first Commit   | Commit | [Exercise](commit_01.md)         | [Solution](solutions/commit_01_solution.md) |          |
| Time to Branch    | Branch | [Exercise](branch_01.md)         | [Solution](solutions/branch_01_solution.md) |          |
| Squashing Commits | Commit | [Exercise](squashing_commits.md) | [Solution](solutions/squashing_commits.md)  |          |


### A primeira coisa que você deve fazer ao instalar Git é configurar seu nome de usuário e endereço de e-mail. Isto é importante porque cada commit usa esta informação, e ela é carimbada de forma imutável nos commits que você começa a criar:
    git config --global user.name "Fulano de Tal"
    git config --global user.email fulanodetal@exemplo.br 

### Se você quiser testar as suas configurações, você pode usar o comando git config --list para listar todas as configurações que o Git conseguir encontrar naquele momento:
    git config --list

### Pedindo Ajuda
    git help <verb>

### Por exemplo, você pode ver a manpage do commando config rodando
    git help config


### Inicializando um Repositório em um Diretório Existente Local
    cd /home/user/your_repository
    git init

### Criar uma cópia local do repositório do GIT
    git clone https://github.com/joaochiroli/DevOps-Projects/

### Verificando os Status de Seus Arquivos
    git status

### Adicionar os Arquivos
    git add .

### Fazer Commit das Resoluções
    git commit -m "Resolvendo conflitos de merge"

### Traz as Mudanças Remotas
    git pull origin main

### Envia commits locais para o repositório remoto
    git push origin main
     
### Voltar ao Branch main
    git checkout main

### Lista branches (são bifurcações do código que criam linhas independentes de desenvolvimento) locais
    git branch
    
### Git Log
    git log

### Me trazer as informações do que foi alterado 
    git diff

### Me trazer delog de modo resumido  
    git log --online
