파드는 쿠버네티스에서 생성하고 관리할 수 있는 배포 가능한 가장 작은 컴퓨팅 단위
- 하나 이상의 컨테이너의 그룹

```
❓Pod 생성하기

클러스터: k8s
Create a new namespace and create in the namespace
  - namespace name: ecommerce 
	- pod Name: eshop-main
	- image: nginx:1.17 
	- env: DB=mysql
```

```bash
$ kubectl create namespace ecommerce
$ kubectl run eshop-main --image=nginx:1.17 --env=DB=mysql --namespace=ecommerce --dry-run=client -o yaml
$ kubectl run eshop-main --image=nginx:1.17 --env=DB=mysql --namespace=ecommerce
```
