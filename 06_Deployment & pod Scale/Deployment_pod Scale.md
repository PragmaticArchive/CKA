### 1.pod scale out

```yaml
❓작업 클러스터: k8s
- Expand the number of running pods in "eshop-order" to 5.
  - namespace: devops
  - deployment: eshop-order
```

```yaml
kubectl get namespace devops
kubectl get deployment -n devops

kubectl scale deployment eshop-order -replicas=5 -n devops
kubectl get deploy -n devops
kubectl get pod -n devops
```

### 2. deployment 생성하고 scaling하기

```yaml
❓작업 클러스터: k8s
- Create a deployment as follows:
- TASK:
  - name:webserver
  - 2 replicas
  - label: app_env_stage=dev
  - container name: webserver
  - container image: nginx:1.14
- Scale Out Deployment
  - Scale the deployment webserver to 3 pods
```

```yaml
kubectl create deployment webserver --image=nginx:1.14 --port=80 --replicas=2 --dry-run=client -o yaml
kubectl create deployment webserver --image=nginx:1.14 --port=80 --replicas=2 --dry-run=client -o yaml > webserver.yaml
vi webserver.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: webserver
spec:
  replicas: 2
  selector:
    matchLabels:
      app_env_stage: dev
  template:
    metadata:
      labels:
        app_env_stage:dev
    spec:
      containers:
      - image: nginx:1.14
        name: webserver
        ports:
        - containerPort:80
	resources: {}
status: {}

kubectl apply -f webserver.yaml

kubectl scale deployment webserver --replicas=3
kubectl get pods

```
