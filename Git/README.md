# GIT


## Git States 


- Modified
- Staged
- Comitted

## Setup and Configuration

- `git init` - Initialize a new Git repository
- git config --global user.name "Fulano de Tal"
- git config --global user.email fulanodetal@exemplo.br
- `git clone <url>` - Clone and create a local copy of a remote repository
- `git config --global <setting_name> <value>` - Configure global Git settings
- `git config <setting_name> <value>` -  Configure local Git settings for a specific repo
- `git config --list` -  Show a summary of your Git configuration settings
- `git config credencial.helper store` -  Configure credentials so you don't have to use a token and password all the time
- `git init --bare` - Initialize a new Git Bare repository
- `git config --global <setting_name> <value>` - Configure global Git settings like 



<div align="center">
  <img src="https://github.com/user-attachments/assets/5af66f50-a44b-4f81-9c6d-9b43b477974b" alt="image" width="350"/>
</div>

## File Operations

- `git status` - Show working tree status
- `git add <file(s)>` - Add files to the staging area
- `git rm <file(s)>` - Remove files from working tree and staging area
- `git mv <old_file> <new_file>` -  Move or rename a file
- `git commit -m "commit message"` -  Commit changes with a message
- `git commit -a -m "commit message"` -  Commit and add file in the same time
- `git commit  -m "Commit" --amend` -  Commit amend. Amend command is a convenient way to modify the most recent commit
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
- `git checkout -- .` - Come back configurations before the add
- `git merge -m <text> <branch>` - Merge. Example **git merge -m "teste" ADDMENU**


<div align="center">
  <img src="https://github.com/user-attachments/assets/4d1fed9c-303b-4990-8bec-7aeb50446ec0" alt="image" width="350"/>
</div>

## Commit History

- `git log` - Show commit history
- `git log --online` - Show commit history with less information
- `git log --since="2 days ago"` - Show commit history of the last 2 days

## Help / Tag / Management

- `git help or git help <verb>` - Show commit history
- `git tag` - List tags
- `git reset --hard <id>` - Discard changes and move HEAD to a specific commit


<div align="center">
  <img src="https://github.com/user-attachments/assets/ea29b64f-c199-4060-9230-57ee45f760ae" alt="image" width="350"/>
  
</div>


## .gitignore
- You can create a file call .gitignore to ignore files

<div align="center">
  <img src="https://github.com/user-attachments/assets/fd370eaf-8971-4dd6-9fdf-d93199035921" alt="image" width="350"/>
  
</div>

    


## Example

```
git add .
git commit -m "Organizando Documento 3.0"
git push -u origin main

```

## Markdown


- `_texto que voce quer_`  - Italic
- `# TEXTO` - Text
- `**TEXTOAQUI**` - Strong/Bold
- `[TEXTO](LINK)` - Link
- `<Propriolink>` - Markdown Link
- `> Fazer a citação` - Citation
- Not Ordenated List
 ``` 
   - Manga 
        - Verde 
    - CAJU
        - Semente
        - UVA 
```

- Ordenated List
 ``` 
     1. Manga 
        1.1. Verde
    2. Uva
        2.1. Argentina
```

- Tables
``` 
Produto | Preço
--------|-------
Coca    | Cola 
```

- Python command

```python
def invert (texto):
```

- Task List
```
- [ ] Acordar
- [ ] Dormir
- [x] Comer
- [x] ~~Almoçar~~ 
```
