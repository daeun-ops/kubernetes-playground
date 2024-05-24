**문제 해설 :** 

- 시험 환경에서는 sudo로 꼭 접속합니다.
- 오래걸리니까 다른문제 풀고 푸세요.

다음과 같이 etcdctl 명령어를  실행해주세요. 

```bash
etcdctl --cacert=옵션값 \
--cert=옵션값 \
--key=옵션값 \
snapshot save 백업파일경로 및 파일명
```

Backup에 필요한 옵션은 3개가 필요한데 --cacert, --cert, --key 이렇게 3개가 필요합니다.

| etcdctl명령 옵션 | etcd프로세스 옵션 | 값 | 비고 |
| --- | --- | --- | --- |
| --cacert | --trusted-ca-file | /etc/kubernetes/pki/etcd/ca.crt | 옵션 이름에 ca가 들어가며 etcd 프로세스에 ca가 들어가는 옵션이 2개(--peer-trusted-ca-file, --trusted-ca-file)가 있는데 가장 마지막 것을 사용 |
| --cert | --cert-file | /etc/kubernetes/pki/etcd/server.crt | 옵션 이름에 공통적으로 cert가 들어가며 cert가 옵션명의 맨 앞에 나옴 |
| --key | --key-file | /etc/kubernetes/pki/etcd/server.key | 옵션 이름에 공통적으로 key가 들어가며 key가 옵션명의 맨 앞에 나옴 |

이렇게 외우기 쉽게 머릿속에 정리를 해두고 이러한 옵션을 사용해서 /opt/etcdbackup 파일로 Backup 파일을 만들 경우 아래와 같이 etcdctl 명령어를 사용하면 됩니다. 

```bash
etcdctl --cacert=/etc/kubernetes/pki/etcd/ca.crt \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key \
snapshot save /opt/etcdbackup
```

이렇게 /opt 디렉토리의 etcdbackup 파일에 ETCD를 백업하게 된다. 약간 암기성으로 접근을 했는데 옵션에 사용된 값 자체를 외우면 안됩니다. 값은 상황에 따라 달라질수 있기 땜에 반드시 옵션명을 기준으로 작업해야합니다.

그러면 이제 이 백업된 파일을 이용해서 ETCD Restore를 진행해야합니다. 

ETCD Restore를 진행할려면 다음과 같이 etcdctl 명령어 작업을 진행해주면됩니다. 

```bash
etcdctl --cacert=옵션값 \
--cert=옵션값 \
--key=옵션값 \
--data-dir=옵션값 \
--initial-advertise-peer-urls=옵션값 \
--initial-cluster=옵션값 \
--name=옵션값 \
snapshot restore 파일경로가 포함된 백업파일 이름
```

Backup 했을때보다 사용해야 할 옵션이 4개가 늘어났습니다. 그러나 --cacert, --cert, --key 옵션은 ETCD Backup 할때도 사용되는 옵션이기 때문에 설정하는데 큰 문제는 없지만  문제는 나머지 4개인데 Backup 할때는 옵션명이 ca, cert, key 요런 단순 문자열이나 그것들의 조합이라 큰 문제가 없지만 Restore는 마땅한 공통점을 찾기 어려워서 외우기 까다로울수도 있기 때문에 아래 추천 영상을 시청하고 시험을 보는 것을 추천드립니다. 

***추천 학습 영상** :* https://www.youtube.com/watch?v=dv_5WCYS5P8

**실제 예시 :** 

*4. Create a snapshot of the existing etcd instance running at **[https://127.0.0.1:2379](https://127.0.0.1:2379/)** saving the snapshot to **/srv/data/etcd-snapshot.db***

*Next, restore an existing, previous snameshot located at **/var/lib/backup/etcd-snapshot-previous.db**.*

*The following TLS certificates/key are supplied for connecting to the server with etcdctl:*

*CA certificate: **/opt/KUIN00601/ca.crt** Client certificate: **/opt/KUIN00601/etcd-client.crt** Clientkey:**/opt/KUIN00601/etcd-client.key***

```docker
backup from etcd:
# ETCDCTL_API=3 etcdctl --endpoints="https://127.0.0.1:2379" --cacert=/opt/KUIN000601/ca.crt --cert=/opt/KUIN000601/etcd-client.crt --key=/opt/KUIN000601/etcd-client.key snapshot save /etc/data/etcd-snapshot.db

restore from etcd:
# ETCDCTL_API=3 etcdctl --endpoints="https://127.0.0.1:2379" --cacert=/opt/KUIN000601/ca.crt --cert=/opt/KUIN000601/etcd-client.crt --key=/opt/KUIN000601/etcd-client.key snapshot restore /var/lib/backup/etcd-snapshot-previoys.db
```
