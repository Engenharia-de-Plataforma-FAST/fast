# Demonstração Kubernetes

Este passo a passo mostra um pouco das capacidades que o kubernetes oferece.

## Setup

Para instalar o minkube, siga os passos 1 e 2 de:  https://minikube.sigs.k8s.io/docs/start/

É possível também utilizar qualquer outro cliente que disponibilize um cluster Kubernetes, por exemplo o [Kind](https://kind.sigs.k8s.io/docs/user/quick-start/), que inclusive ja vem instalado com o docker desktop. Também é possível utilizar o [GKE](https://cloud.google.com/kubernetes-engine/docs/deploy-app-cluster).

É necessário também instalar o kubectl. Escolha de acordo com o sistema operacional da sua máquina: https://kubernetes.io/docs/tasks/tools/ 

## Conhecendo o kubectl

Com o kubectl é possível interagir com clusters kubernetes. Alguns comandos importantes: 

* **get**: Lista informações gerais sobre entidades
* **describe**: Lista informações específicas sobre uma entidade
* **edit**: Edita o YAML de uma entidade
* **create**: Cria uma nova entidade
* **delete**: Deleta uma entidade
* **apply**: Aplica um arquivo de configuração Yaml.
* **logs**:  Mostra os logs de containers/pods/deployments
* **exec**: Executa um comando em um container específico
* **port-forward**: Espelha uma porta local com a porta de um serviço rodando no cluster.

### Namespace
#### Listando os namespaces:

```bash
kubectl get namespaces # ou ns
```

#### Criando um novo namespace:

```bash
kubectl create namespace fast
```

#### Descrevendo mais detalhes de um namespace:

```bash
kubectl describe namespace fast
```

### Pods

#### Listando os pods:

```bash
kubectl get pods --all-namespaces # ou -A
```

```bash
kubectl get pods --namespace fast # ou -n
```


#### Criando um pod no namespace fast:

```yaml
# pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  namespace: fast # por padrao ficaria no ns default
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80
```

```bash
kubectl apply -f pod.yaml
```

#### Listando os pods com mais informações:

```bash
kubectl get pods --all-namespaces -o wide 
```

#### Criando um pod com múltiplos containers:
```yaml
# pod-multicontainer.yaml
apiVersion: v1
kind: Pod
metadata:
  name: multicontainer
  namespace: fast # por padrao ficaria no ns default
spec:
  containers:
    - name: nginx
      image: nginx:1.14.2
      ports:
      - containerPort: 80
    - name: hello
      image: busybox:1.28
      command: ['sh', '-c', 'echo "Hello, Kubernetes!" && sleep 3600']
```

```bash
kubectl apply -f pod-multicontainer.yaml
```

Ver informações de cada container
```bash
kubectl describe pod multicontainer -n fast
```

### ReplicaSets

```yaml
# replica-set.yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx
  namespace: fast
  labels:
    app: hello-world-nginx
    tier: nginx
spec:
  # modifique o número de replicas de acordo com o seu caso
  replicas: 3
  selector:
    matchLabels:
      tier: nginx
  template:
    metadata:
      labels:
        tier: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:1.14.2
          ports:
          - containerPort: 80
```

Listando informações do replica set:

```bash
kubectl get replicaset -n fast # ou rs
```

```bash
kubectl describe rs/nginx -n fast
```

Deletando um pod criado e vendo o que acontece:
```bash
kubectl delete pod/nginx-<id> -n fast
kubectl get pods -n fast
```

### Deployments

```yaml
#  deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

```bash
kubectl get deployments -n fast
```

```bash
kubectl get rs -n fast
```

```bash
kubectl get pods -n fast
```

### Services

```bash
kubectl expose deployment/nginx-deployment --port=80 --type=NodePort
```

// [TODO] ver como a gente pode ostrar acessando uma URL atra'ves do service.

### Jobs

### Cronjobs
