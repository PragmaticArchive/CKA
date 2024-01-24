```yaml
❓Check to see how many nodes are ready(not including nodes tainted NoSchedule) and write the number to /var/CKA2022/RN0001
```

```yaml
$ kubectl get nodes | grep -i -w ready
$ kubectl describe nodes hk8s-m | grep -i NoSchedule
$ kubectl describe node hk8s-w1 | grep -i NoSchedule
$ kubectl describe node hk8s-w1 | grep -i taints
$ echo "1" > /var/CKA2022/RN0001
```

- -w(word) ready를 가지고 있는 node 출력
- Noschedule이나 taint정보가 있는지 확인


```yaml
❓Determine how maney nodes in the cluster are ready to run normal workloads(i.e, workloads that do not have any special tolerations).
Output the number to the file /var/CKA2022/NODE-Count
```

```yaml
$ kubectl get nodes | grep -i -w ready | wc -l > /var/CKA2022/NODE-Count
$ cat /var/CKA2022/NODE-Count
```

- -w ready ⇒ ready를 포함하고 있는 String 검색
- wc -l 몇개인지 출력
