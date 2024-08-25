# AWS

#### IAM 

- IAM = Gerenciamento de Identidade e Acesso, serviço global
- Conta ROOT criada por padrão, não deve ser usada nem compartilhada
- Usuários são pessoas dentro da sua organização e podem ser agrupados
- Grupos contêm apenas usuários, não outros grupos
- Usuários não precisam pertencer a um grupo e um usuário pode pertencer a vários grupos.

#### SDK - Boto3

- Uma ferramenta que permite interagir com os serviços da AWS usando comandos em seu Shell de linha de comando
- Acesso direto às APIs públicas dos serviços da AWS
- É possível desenvolver scripts para gerenciar seus recursos
- É de código aberto (open-source) em https://github.com/aws/aws-cli
- Alternativa ao uso da Console de Gerenciamento da AWS

#### Network - VPC

- Subnets:
    - Public Subnet: Subrede que tem acesso à internet, geralmente usada para recursos que precisam ser acessados publicamente, como servidores web.
    - Private Subnet: Subrede isolada da internet, usada para recursos que não precisam de acesso direto à internet, como bancos de dados.
- Internet Gateway (IGW):
    - Componente que permite que os recursos em uma VPC com subredes públicas possam se comunicar com a internet.
- NAT Gateway:
    - Permite que instâncias em subredes privadas acessem a internet de forma segura, enquanto bloqueia o tráfego de entrada não solicitado.
- Security Groups:
    - Firewall virtual que controla o tráfego de entrada e saída das instâncias da EC2 dentro da VPC. Funciona no nível da instância.
- Network ACLs (NACLs):
    - Lista de controle de acesso que atua como uma camada de segurança adicional para sua VPC, controlando o tráfego que entra e sai das subnets. Funciona no nível da subnet.
- VPC Peering:
    - Conexão de rede entre duas VPCs que permite que o tráfego roteado entre elas se comunique de forma privada.
- VPN Gateway:
    - Gateway que permite estabelecer uma conexão segura entre a sua VPC e uma rede corporativa on-premises através de uma VPN (Virtual Private Network).
- Route Tables:
    - Tabelas de rotas que determinam para onde o tráfego de rede deve ser direcionado, baseado no destino.
- VPC Endpoints:
    - Permite que você se conecte de forma privada a serviços da AWS sem precisar de um gateway de internet, NAT, VPN, ou conexão Direct Connect.
- VPC Flow Logs:
    - Permite capturar informações sobre o tráfego IP indo de e para interfaces de rede na VPC.

#### EC2

AWS EC2

- EC2 é uma das ofertas mais populares da AWS.
- EC2 = Elastic Compute Cloud = Infraestrutura como Serviço.
- Consiste principalmente na capacidade de:
- Alugar máquinas virtuais (EC2).
- Armazenar dados em unidades de armazenamento virtual (EBS).
- Distribuir a carga entre as máquinas (ELB).
- Dimensionar os serviços usando um grupo de dimensionamento automático (ASG).
