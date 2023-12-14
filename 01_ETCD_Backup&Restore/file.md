### ETCD

<aside>
❓ **ETCD Backup&Restore
작업 시스템: k8s-master
First, create a snapshot of the existing etcd instance running at https://127.0.0.1:2379, saving the snapshot to /data/etcd-snapshot.db.
Next, restore an existing, previous snapshot located at /data/etcd-snapshot-previous.db.

The following TLS certificates/key are supplied for connecting to the server with etcdctl:
CA certificate: /etc/kubernetes/pki/etcd/ca.crt
Client certifiate: /etc/kubernetes/pki/etcd/server.crt
Client key: /etc/kubernetes/pki/etcd/server.key**

</aside>

```yaml
1. ETCD를 호스팅할 시스템 ssh 로그인
	ssh k8s-master

동작중인 etcd 버전과 etcdctl 툴 설치여부 확인
etcd --version
etcdctl version

2. etcd Backup
sudo ETCDCTL_API=3 etcdctl --endpoints=https://127.0.0.1:2379 \
  --cacert=**/etc/kubernetes/pki/etcd/ca.crt** \
	--cert=**/etc/kubernetes/pki/etcd/server.crt** \
	--key=**/etc/kubernetes/pki/etcd/server.key** \
  snapshot save **/data/etcd-snapshot.db

3. etcd Restore
ETCDCTL_API=3 etcdctl --data-dir=/var/lib/etcd-previous snapshot restore /data/etcd-snapshot-previous.db**

```
