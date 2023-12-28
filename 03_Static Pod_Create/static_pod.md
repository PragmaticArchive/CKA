### Pod 동작방식

1. k8s 구성요소 (master node1 node2) 노드들이 존재
2. 사용자의 kubectl nginx pod 생성 요청 → API Controller 전달
3. API Controller는 요청을 받으면 etcd의 상태 정보를 꺼내서 scheduler에게 전달
4. scheduler를 통해 생성에 적합한 node 선별 후 가장 적합한 node를 선택 후 api에게 알려줌
5. node1를 선택했다면 API Controller에서 node1의 kubelet에게 명령 전달
6. 각각의 노드에는 컨테이너 엔진이 존재
7. kubelet이 컨테이너 엔진에게 요청해서 pod를 생성
8. 실행된 상태정보를 다시 kubelet에게 전달하고 kubelet은 API에게 상태정보 전달
9. API는 현재 node1의 pod 실행정보를 etcd에 저장

### static pod 동작방식

1. API 컨트롤러의 도움을 받지 않고 동작하지 않음, 각 노드의 해당 kubelet에게 요청
2. kubelet은 자신만의 config 파일을 가지고 있음 /var/lib/kubelet/config.yaml을 기반으로 데몬 동작
3. 해당 노드의 /etcd/kubernetes/manifests → 위치에 static pod yaml 파일 생성, 저장하면 yaml 파일 기준으로 kubelet이 static pod 실행

```
❓ Configure kubelet hosting to start a pod on the node
TASK:
 - Node: hk8s-w1
 - pod Name: web
 - Image: nginx
```

```
kubelet run web --image=nginx --dry-run=client -o yaml
ssh hk8s-w1
sudo -i
cd /etc/kubernetes/manifests
cat > web.yaml

apiVersion: v1
kind: Pod
metadata:
 name: web
spec:
 containers:
 - image:nginx
   name: web
```
