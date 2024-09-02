# Day one

### Ec2 Simples
![image](https://github.com/user-attachments/assets/fa22943b-c3d9-449a-9f93-b21f0547246f)


 - Criar VPC - 10.0.0.0/16
 - Subnet - 10.0.0.0/24
     - edit settings e clique em Enable auto-assign public IPv4 address
 - Criar Security Group - permissão para 80 e 22
 - Criar Internet Gateway
 - Criar Route Table
    - Atachar as subnets
    - Criar route table para saida pra internet 0.0.0.0/0
 - Implementar EC2
   

### ELB com 2 instancias e alta disponibilidade
![image](https://github.com/user-attachments/assets/167bbca7-3b01-4956-9442-42afbcfbcae4)

 - Como já criamos um Internet Gateway e rotas publicas para ele podemos reutilizar
 - Criar uma subnet
 - Criar uma outra EC2
 - Criar um Load Balancer e seus targets

### RDS com read replica

![image](https://github.com/user-attachments/assets/83846717-8a62-491f-96cf-d982662bfdda)
