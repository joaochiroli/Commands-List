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

### VocÊ pode adicionar colaboradores ao seu projeto 
    precisa ir té a interface web do github e dar as permissões
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
     
### Voltar ao Branch principal
    git checkout main ou git checkout master

### Voltar ao commit
    git checkout <id do commit>

### Lista branches (são bifurcações do código que criam linhas independentes de desenvolvimento) locais
    git branch
    
### Git Log
    git log

### Me trazer as informações do que foi alterado 
    git diff

### Me trazer delog de modo resumido  
    git log --online

### Fazendo o commit junto com o add 
    git commit  -a -m "Commit"

### Git tem basicamente 3 estados 
    Working / Staging / Commit

### Restaurar arquivo 
    git restore <estado> <arquivo>

### Renomear arquivo
    git mv <arquivo1> <arquivo2>

### Realizar um amend na mensagem 
    git commit  -m "Commit" --amend

### Desafazendo as coisas (atualização no mesmo commit)
    git commit --amend -m "Atualização necessaria para criação de novo arquivo"

![image](https://github.com/user-attachments/assets/ea29b64f-c199-4060-9230-57ee45f760ae)

### Voltar um estado da configuração 
    git reset --hard <id>

### Criar um atalho no Git
![image](https://github.com/user-attachments/assets/dea08482-122b-4d46-86f5-e4f5735fff1c)

### Boas práticas
    Nunca trabalhar em cima da branch main 

![image](https://github.com/user-attachments/assets/efda13de-4414-4422-8e51-21602b5ad1ce)

### Checar a branch 
    git branch

### Criar branch 
    git branch ADDMENU

### Mudar a branch 
    git switch <nome da branch>

### Passar o conteudo de uma branch para a main, entrar na branch main e fazer o comando abaixo
    git merge -m "teste" ADDMENU

### Remover Branch
    git branch -d ADDMENU

### Remova o repositório remoto:
    git remote remove origin

### Criar novo repo 
    git init 
    git add README.md
    git commit -m "first commit"
    git branch -M main
    git remote add origin https://github.com/joaochirolit/Git-Curso.git
    git push -u origin main

    origin é o repositorio remoto, voce pode descobrir usando o comando git remote -v
    main é a branch

## Push um repositorio existente 
    git remote add origin https://github.com/joaochirolit/Git-Curso.git
    git brach -M main
    git push -u origin main 

## Voce pode criar um arquivo chamado .gitignore para ignorar 
![image](https://github.com/user-attachments/assets/fd370eaf-8971-4dd6-9fdf-d93199035921)

## Log 2 dias atras 
    git log --since="2 days ago"


## Git bare (você está criando um repositório que é pushable. Geralmente os repositórios bare são criados no servidor e são considerados repositórios para armazenamento)
    git init --bare 


![image](https://github.com/user-attachments/assets/5af66f50-a44b-4f81-9c6d-9b43b477974b)

## Listar tag
    git tag 

## Nova tag
    git push origin v1.0

## Configurar credencial para nao ficar usando token e senha toda hora
    git config credencial.helper store

## Voltar as configurações antes de fazer o add 
    git checkout -- .
    
    ![image](https://github.com/user-attachments/assets/4d1fed9c-303b-4990-8bec-7aeb50446ec0)

## Markdown itálico 
    _texto que voce quer_

## Markdown titulo 
    # TEXTO

## Strong/Bold vulgo negrito
    **TEXTOAQUI**

## Markdown Link
    [TEXTO](LINK)

## Markdown Link
    <Propriolink>

## Citação 
    > Fazer a citação

## Lista não ordenada 
    - Manga 
        - Verde 
    - CAJU
        - Semente
        - UVA 

## Listas Ordenadas
    1. Manga 
        1.1. Verde
    2. Uva
        2.1. Argentina

## Tabelas 

Produto | Preço
--------|-------
Coca    | Cola 
    
## Python command 

```python
def invert (texto):
```
