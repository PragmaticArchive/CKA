```yaml
❓create pod
- 작업 클러스터: hk8s
- create a pod named lab004 with 3 containers runnig: nginx, redis, memcached
```

```yaml
kubectl run lab004 --image=nginx --dry-run=client -o yaml > multi.yaml

apiVersion: v1
kind: Pod
metadata:
 name: lab004
spec:
 containers:
 - image: nginx
   name: nginx
 - image: redis
   name: redis
 - image: memcached
   name: memcached 

kubectl apply -f multi.yaml
```
