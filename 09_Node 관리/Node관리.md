```yaml
❓작업 클러스터: k8s-worker1
   - Set the node named k8s-worker1 as unavailable and reschedule all the pods running on it.
```

```yaml
$ kubectl drain k8s-worker1 --ignore-daemonsets --force
$ kubectl get nodes
$ kubectl get pods -o wide
```

- drain을 통해 해당 노드에 존재하는 pod를 제거
- docker cni와 관련있는(kube-flannel, kube-proxy) daemonset(worker node당 하나씩만 실행)의 경우 삭제할 수 없다는 오류가 발생하는데 —ignore-daemonsets 옵션을 추가해서 drain을 진행할 수 있다.
