# GIT


## Git States 


- Modified
- Staged
- Comitted

## Setup and Configuration

- `git init` - Initialize a new Git repository
- `git clone <url>` - Clone and create a local copy of a remote repository
- `git config --global <setting_name> <value>` - Configure global Git settings
- `git config <setting_name> <value>` -  Configure local Git settings for a specific repo
- `git config --list` -  Show a summary of your Git configuration settings

## File Operations

- `git status` - Show working tree status
- `git add <file(s)>` - Add files to the staging area
- `git rm <file(s)>` - Remove files from working tree and staging area
- `git mv <old_file> <new_file>` -  Move or rename a file
- `git commit -m "commit message"` -  Commit changes with a message
- `git commit -a -m "commit message"` -  Commit and add file in the same time
- `git diff` -  Show differences between working tree and last commit


## Remote Repositories

- `git remote -v` - List remote repositories
- `git pull <remote_name> <remote_branch>` - Pull changes from a remote branch, example **git pull origin main**
- `git push -u <remote_name> <local_branch>` - Push changes to a remote repository, example **git push -u origin main**

## Example

```
git add .
git commit -m "Organizando Documento 3.0"
git push -u origin main

```

### VocÊ pode adicionar colaboradores ao seu projeto 
    precisa ir té a interface web do github e dar as permissões
### Pedindo Ajuda
    git help <verb>

### Por exemplo, você pode ver a manpage do commando config rodando
    git help config
     
### Voltar ao Branch principal
    git checkout main ou git checkout master

### Voltar ao commit
    git checkout <id do commit>

### Lista branches (são bifurcações do código que criam linhas independentes de desenvolvimento) locais
    git branch
    
### Git Log
    git log

### Me trazer delog de modo resumido  
    git log --online

### Restaurar arquivo 
    git restore <estado> <arquivo>

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

## Lista de tarefas

- [ ] Acordar
- [ ] Dormir
- [x] Comer
- [x] ~~Almoçar~~ 
