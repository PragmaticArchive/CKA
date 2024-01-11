```yaml
❓작업 클러스터: k8s
- create a deployment as follows:
- TASK:
  - name: nginx-app
  - Using container nginx with version 1.11.10-alpine
  - The deployment shold contain 3 replicas
- Next, deploy the application with new version 1.11.13-alpine, by performing a rolling update
- finally, rollback that update to the previous version 1.11.10-alpine
```

```yaml
kubectl create deployment nginx-app 00image=nginx:1.11.10-alpine --replicas=3 --dry-run=client -o yaml
kubectl get deployments.apps nginx-app
kubectl set image deployment nginx-app nginx=nginx:1.11.13-alpine --record

kubectl rollout history deployment nginx-app
kubectl rollout undo deployment nginx-app
kubectl rollout history deployment nginx-app
```
