```yaml
❓작업 클러스터: kubectl config use-context k8s
- Schedule a pod as follows:
  - name: eshop-store
  - Image: nginx
  - Node selector: disktype=ssd
```

```yaml
worker node의 label 확인
$ kubectl get node --show-labels
$ kubectl get node -L disktype

disktype=ssd 레이블을 가지고 있는 node에서 pod가 실행되도록 스케줄링
$ kubectl run eshop-store --image-nginx --dry-run=client -o yaml
$ kubectl run eshop-store --image-nginx --dry-run=client -o yaml > eshop-store.yaml
$ vi eshop-store.yaml
apiVersion: v1
kind: Pod
metadata:
  name: eshop-store
spec:
  nodeSelector:
    disktype: ssd
  containers:
  - image: nginx
    name: eshop-store
$ kubectl apply -f eshop-store.yaml
$ kubectl get pod eshop-store -o wide
```

- node의 labels를 통해 nodeselector값 찾기
- -L disktype를 통해 label중 disktype을 key로 갖는 label 추출
