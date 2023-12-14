### ETCD
- key:value형태의 데이터를 저장하는 스토리지
- k8s를 위한 구성데이터, 상태 데이터, 메타데이터를 관리
- Kubernetes API 서버는 각 클러스터의 상태 데이터를 etcd에 저장
- 현재 동작중인 k8s의 모든 운영정보를 담고있음 그래서 백업이 필요함

```yaml
❓ ETCD Backup & Restore
작업 시스템: k8s-master
First, create a snapshot of the existing etcd instance running at https://127.0.0.1:2379, saving the snapshot to /data/etcd-snapshot.db.
Next, restore an existing, previous snapshot located at /data/etcd-snapshot-previous.db.

The following TLS certificates/key are supplied for connecting to the server with etcdctl:
CA certificate: /etc/kubernetes/pki/etcd/ca.crt
Client certifiate: /etc/kubernetes/pki/etcd/server.crt
Client key: /etc/kubernetes/pki/etcd/server.key

```

```yaml
1. ETCD를 호스팅할 시스템 ssh 로그인
ssh k8s-master

동작중인 etcd 버전과 etcdctl 툴 설치여부 확인
etcd --version
etcdctl version

2. etcd Backup
sudo ETCDCTL_API=3 etcdctl --endpoints=https://127.0.0.1:2379 \
--cacert=/etc/kubernetes/pki/etcd/ca.crt \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key \
  snapshot save /data/etcd-snapshot.db

3. etcd Restore
ETCDCTL_API=3 etcdctl --data-dir=/var/lib/etcd-previous snapshot restore /data/etcd-snapshot-previous.db**

```
