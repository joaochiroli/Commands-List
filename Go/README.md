- Ao executar comandos como go build ou go mod tidy, o Go baixa automaticamente as dependências necessárias conforme especificadas no go.mod e mantém um cache local

- Inicializar alicação Go
- go mod init api-mdc-go

Quando você executa go mod init, o Go cria um arquivo chamado go.mod, que é usado para gerenciar as dependências do seu projeto e as versões de bibliotecas que ele usa. 

Após o go.mod ter sido criado (normalmente por go mod init) e você ter adicionado dependências ao projeto (através de go get ou go mod tidy), o comando go mod download baixa as dependências especificadas para o cache local, permitindo que o projeto seja compilado ou executado corretamente.
