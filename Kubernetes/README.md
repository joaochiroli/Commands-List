Aqui está uma explicação de cada termo relacionado ao Kubernetes:

1. **Pod**: É a menor e mais simples unidade em Kubernetes. 

2. **ReplicaSet**: Garante que um número específico de réplicas (instâncias) de um determinado pod esteja rodando em qualquer momento. Se um pod falhar, o ReplicaSet cria um novo para substituí-lo, mantendo a quantidade de réplicas desejada

3. **Deployment**: Controla a criação e o gerenciamento de ReplicaSets. Permite fazer atualizações ou reversões controladas nas aplicações sem interrupção. O Deployment facilita o rollout de novas versões de um aplicativo e o rollback caso algo dê errado.

4. **Service**: Expõe um conjunto de pods como um serviço de rede único. Ele define uma política de acesso (como balanceamento de carga) para os pods que correspondem a um conjunto de critérios (normalmente com base em seletores de rótulos). O **Service** permite que os pods se comuniquem entre si ou com o mundo externo de forma consistente, mesmo que os pods individuais sejam criados e destruídos.

5. **LoadBalancer**: Um tipo específico de **Service** que expõe os serviços de aplicativos para fora do cluster, criando um balanceador de carga externo.

6. **Disk**: Refere-se ao armazenamento persistente no Kubernetes, geralmente usando um **PersistentVolume** e um **PersistentVolumeClaim**. Isso permite que os dados de um pod sobrevivam ao término ou recriação do pod. Discos podem ser montados em pods para armazenar dados que devem persistir além da vida útil do próprio pod.

7. **Ingress**: Gerencia o acesso externo aos serviços no Kubernetes, fornecendo regras de roteamento de entrada (HTTP/HTTPS). O **Ingress** permite definir como as solicitações externas são roteadas para serviços internos com base em regras como subdomínios, caminhos e hosts. Ele também pode lidar com SSL/TLS, permitindo configurações HTTPS.

8. **Health Check**: São verificações de saúde que o Kubernetes usa para garantir que os contêineres dentro de um pod estejam funcionando corretamente. Existem dois tipos principais:
   - **Liveness probe**: Verifica se o aplicativo está vivo e em funcionamento. Se falhar, o Kubernetes reinicia o contêiner.
   - **Readiness probe**: Verifica se o aplicativo está pronto para receber tráfego. Se falhar, o Kubernetes remove temporariamente o pod da lista de serviços disponíveis.

9. **CronJob**: Executa **Jobs** em horários ou intervalos específicos, semelhantes a cron jobs no Linux. Um **CronJob** é útil para tarefas recorrentes, como backups periódicos ou envios de relatórios. Ele agendará e gerenciará a execução automática dos **Jobs** com base em uma programação definida.
    
10. KEDA

#### Install ####

Kubectl: Ferramenta genérica para interagir e gerenciar os recursos dentro de qualquer cluster Kubernetes. Ele é usado principalmente dentro do cluster, manipulando objetos como pods, serviços, deployments, etc.

```
curl -LO "https://dl.k8s.io/release/$(curl -Ls https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
kubectl version --client
```

Eksctl: Ferramenta específica para gerenciar clusters no Amazon EKS, sendo responsável por provisionar, gerenciar e destruir clusters e suas infraestruturas associadas no AWS.

```
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version

```

LoadBalancer 

```
apiVersion: v1
kind: Service
metadata:
  name: myapp1-loadbalancer
  labels: 
    app: myapp1
spec:
  type: LoadBalancer 
  selector:
    app: myapp1
  ports: 
    - port: 80
      targetPort: 5000
```

Deployment 
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp1-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp1
  template: 
    metadata:
      name: myapp1-pod
      labels:
        app: myapp1       
    spec:
      containers:
        - name: myapp1-container
          image: iesodias/mdc-api-python:latest
          ports:
            - containerPort: 5000
```
