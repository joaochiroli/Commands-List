Aqui está uma explicação de cada termo relacionado ao Kubernetes:

1. **Pod**: É a menor e mais simples unidade em Kubernetes. 

2. **ReplicaSet**: Garante que um número específico de réplicas (instâncias) de um determinado pod esteja rodando em qualquer momento. Se um pod falhar, o ReplicaSet cria um novo para substituí-lo, mantendo a quantidade de réplicas desejada

3. **Deployment**: Controla a criação e o gerenciamento de ReplicaSets. Permite fazer atualizações ou reversões controladas nas aplicações sem interrupção. O Deployment facilita o rollout de novas versões de um aplicativo e o rollback caso algo dê errado.

4. **Service**: Expõe um conjunto de pods como um serviço de rede único. Ele define uma política de acesso (como balanceamento de carga) para os pods que correspondem a um conjunto de critérios (normalmente com base em seletores de rótulos). O **Service** permite que os pods se comuniquem entre si ou com o mundo externo de forma consistente, mesmo que os pods individuais sejam criados e destruídos.
   - **ClusterIP (Padrão)**: Descrição: O serviço é exposto internamente apenas dentro do cluster Kubernetes. Uso: Ideal para comunicação interna entre diferentes aplicações ou componentes dentro do cluster. Como funciona: O Kubernetes atribui um IP interno para o serviço, acessível apenas dentro do cluster. Outros pods podem se comunicar com o serviço através desse IP.
   - **NodePort**: Descrição: Expõe o serviço externamente usando uma porta específica em cada nó do cluster. Uso: Utilizado quando você precisa de acesso externo básico ao cluster, mas sem um balanceador de carga gerenciado por um provedor de nuvem. Como funciona: O Kubernetes abre uma porta no intervalo 30000-32767 em cada nó e redireciona o tráfego dessa porta para os pods associados ao serviço.
   - **LoadBalancer**: Um tipo específico de **Service** que expõe os serviços de aplicativos para fora do cluster, criando um balanceador de carga externo. Descrição: Cria automaticamente um balanceador de carga externo, fornecido por serviços de nuvem (como AWS, Azure, GCP), e direciona o tráfego para o serviço. Uso: Quando você precisa de acesso externo ao serviço com balanceamento de carga gerenciado, útil para expor aplicativos para a internet. Como funciona: O provedor de nuvem cria um balanceador de carga que distribui o tráfego entre os nós do cluster e os redireciona para os pods por meio de um NodePort ou ClusterIP.
   - **ExternalName**: Descrição: Mapeia um serviço interno para um nome DNS externo. Uso: Quando você deseja acessar serviços externos ao cluster (como APIs de terceiros) sem sair do contexto do cluster. Como funciona: Redireciona para um nome DNS (como uma API externa ou serviço) sem expor diretamente nenhum recurso interno.

6. **Disk**: Refere-se ao armazenamento persistente no Kubernetes, geralmente usando um **PersistentVolume** e um **PersistentVolumeClaim**. Isso permite que os dados de um pod sobrevivam ao término ou recriação do pod. Discos podem ser montados em pods para armazenar dados que devem persistir além da vida útil do próprio pod.

7. **Ingress**: Gerencia o acesso externo aos serviços no Kubernetes, fornecendo regras de roteamento de entrada (HTTP/HTTPS). O **Ingress** permite definir como as solicitações externas são roteadas para serviços internos com base em regras como subdomínios, caminhos e hosts. Ele também pode lidar com SSL/TLS, permitindo configurações HTTPS.

8. **Health Check**: São verificações de saúde que o Kubernetes usa para garantir que os contêineres dentro de um pod estejam funcionando corretamente. Existem dois tipos principais:
   - **Liveness probe**: Verifica se o aplicativo está vivo e em funcionamento. Se falhar, o Kubernetes reinicia o contêiner.
   - **Readiness probe**: Verifica se o aplicativo está pronto para receber tráfego. Se falhar, o Kubernetes remove temporariamente o pod da lista de serviços disponíveis.

9. **CronJob**: Executa **Jobs** em horários ou intervalos específicos, semelhantes a cron jobs no Linux. Um **CronJob** é útil para tarefas recorrentes, como backups periódicos ou envios de relatórios. Ele agendará e gerenciará a execução automática dos **Jobs** com base em uma programação definida.
    
10. KEDA

11. O HPA (Horizontal Pod Autoscaler) é um recurso do Kubernetes que ajusta automaticamente o número de réplicas de pods em um Deployment, ReplicaSet, StatefulSet ou ReplicationController com base na utilização de recursos, como CPU ou memória, ou em métricas personalizadas.
    


#### Commands ####

- `kubectl exec -it <pod-name> -- sh` Connecting to container in a POD
- `kubectl get pod mdc-app -o yaml` Get pod definition YAML output
- `kubectl exec -it <pod-name> -- env` Running individual commands in a Container example
   - kubectl exec -it mdc-app -- env
   - kubectl exec -it mdc-app -- ls
   - kubectl exec -it mdc-app -- cat /app/templates_folder/mdc.html
- `kubectl get replicaset` or `kubectl get rs`
- `kubectl describe rs`
- `kubectl get pods -o wide` Get list of Pods with Pod IP and Node in which it is running
- `kubectl get pods POD_NAME -o yaml` verify the owner of pod
- `kubectl expose rs <ReplicaSet-Name>  --type=LoadBalancer --port=80 --target-port=8080 --name=<Service-Name-To-Be-Created>` Expose ReplicaSet as a Service
- `kubectl scale --replicas=10 deployment/<Deployment-Name>` Scale Up the Deployment
- `kubectl edit deploy -n mdc-app` edit Deployment
- `kubectl run apache-bench -i --tty --rm --image=httpd -- ab -n 500000 -c 1000 http://YOUR_IP/mdc` Generate load 

      

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
  name: myapp1-deployment # define o nome do deployment
spec:
  replicas: 2 
  selector:
    matchLabels:
      app: myapp1 # Usados para associar os pods que o Deployment gerencia
  template: # block defines the Pod template that the Deployment will use to create its replicas
    metadata:
      name: myapp1-pod # define o nome do pod
      labels:
        app: myapp1 # define a label do pod
    spec:
      containers:
      - name: myapp1-container # This gives a name to the container running inside the pod
        image: iesodias/mdc-api-python:latest
        ports:
          - containerPort: 5000 # This means that port 5000 will be exposed inside the container
```

Autoscaling
```
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: mdc-app
  namespace: mdc-app
spec:
  maxReplicas: 20 # define max replica count
  minReplicas: 1  # define min replica count
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: mdc-app
  targetCPUUtilizationPercentage: 10 # target CPU utilization
```

Service
```
apiVersion: v1
kind: Service
metadata:
  name: mdc-app
  namespace: mdc-app
  labels:
    app: mdc-app
spec:
  type: ClusterIP
  selector:
    app: mdc-app
  ports:
    - port: 80
      targetPort: 5000
```
