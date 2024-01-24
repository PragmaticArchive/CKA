https://kubernetes.io/docs/concepts/services-networking/service/

```yaml
❓작업 클러스터: kubectl config use-context k8s
- Reconfigure the deployment front-end and add a port specification named http exposing port 80/tcp of the existing container nginx.
  create a new service named front-end-svc exposing the container port http.
  Configure the new service to also expose the individual Ports via a NodePort on the nodes on which they are scheduled
```

```yaml
$ kubectl get deployments.apps front-end
$ kubectl get deployments.apps front-end > front-end.yaml
$ vi front-end.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: front-end
spec:
  replicas: 2
  selector:
    matchLabels:
      run: nginx
  template:
    metadata:
      labels:
        run: nginx
    spec:
      containers:
      - image: nginx
        name: http
        ports:
        - containerPort: 80
          name: http

---
apiVersion: v1
kind: Service
metadata:
  name: front-end-svc
spec:
  type: NodePort
  selector:
    run: nginx
  ports:
  - name: http
    protocol: TCP
    port: 80
    targetPort: http

$ kubectl delete deploy front-end
$ kubectl apply -f front-end.yaml
$ curl k8s-worker1:#####
```

- Service는 type: NodePort를 가짐
- targetPort를 deployment의 http포트를 target으로 잡음
