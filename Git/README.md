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
- `git init --bare` - Initialize a new Git Bare repository

![image](https://github.com/user-attachments/assets/5af66f50-a44b-4f81-9c6d-9b43b477974b)

## File Operations

- `git status` - Show working tree status
- `git add <file(s)>` - Add files to the staging area
- `git rm <file(s)>` - Remove files from working tree and staging area
- `git mv <old_file> <new_file>` -  Move or rename a file
- `git commit -m "commit message"` -  Commit changes with a message
- `git commit -a -m "commit message"` -  Commit and add file in the same time
- `git commit  -m "Commit" --amend"` -  Commit amend. Amend command is a convenient way to modify the most recent commit
- `git diff` -  Show differences between working tree and last commit
- `git restore <estado> <arquivo>` -  Restore the file


## Remote Repositories / Branch / Merge

- `git remote -v` - List remote repositories
- `git pull <remote_name> <remote_branch>` - Pull changes from a remote branch, example **git pull origin main**
- `git push -u <remote_name> <local_branch>` - Push changes to a remote repository, example **git push -u origin main**
- `git branch` - List all branches
- `git branch <name>` - Create a branch
- `git branch -d <name>` - Remove a branch
- `git checkout <commit or branch>` - Switch to a specific branch or commit
- `git merge -m <text> <branch>` - Merge. Example **git merge -m "teste" ADDMENU**




## Commit History

- `git log` - Show commit history
- `git log --online` - Show commit history with less information
- `git log --since="2 days ago"` - Show commit history of the last 2 days

## Help

- `git help or git help <verb>` - Show commit history


### VocÊ pode adicionar colaboradores ao seu projeto 
    precisa ir té a interface web do github e dar as permissões


![image](https://github.com/user-attachments/assets/ea29b64f-c199-4060-9230-57ee45f760ae)

### Voltar um estado da configuração 
    git reset --hard <id>

### Criar um atalho no Git
![image](https://github.com/user-attachments/assets/dea08482-122b-4d46-86f5-e4f5735fff1c)

### Boas práticas
    Nunca trabalhar em cima da branch main 

![image](https://github.com/user-attachments/assets/efda13de-4414-4422-8e51-21602b5ad1ce)



### Passar o conteudo de uma branch para a main, entrar na branch main e fazer o comando abaixo
    git merge -m "teste" ADDMENU


## Voce pode criar um arquivo chamado .gitignore para ignorar 
![image](https://github.com/user-attachments/assets/fd370eaf-8971-4dd6-9fdf-d93199035921)



## Listar tag
    git tag 

## Nova tag
    git push origin v1.0

## Configurar credencial para nao ficar usando token e senha toda hora
    git config credencial.helper store

## Voltar as configurações antes de fazer o add 
    git checkout -- .
    
    ![image](https://github.com/user-attachments/assets/4d1fed9c-303b-4990-8bec-7aeb50446ec0)

## Example

```
git add .
git commit -m "Organizando Documento 3.0"
git push -u origin main

```

------------------------------------------------------------------

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
