# Docker 서비스 자동 시작방법

systemctl enable docker.service

```
[root@bi-test system]# systemctl enable docker.service
Created symlink from /etc/systemd/system/multi-user.target.wants/docker.service to /usr/lib/systemd/system/docker.service.
```
시스템 부팅시 자동 시작되는 서비스 리스트 출력 
systemctl list-unit-files --type service | grep enabled

```
[root@bi-test systemd]# systemctl list-unit-files --type service | grep enabled
auditd.service                                enabled
autovt@.service                               enabled
crond.service                                 enabled
dbus-org.freedesktop.nm-dispatcher.service    enabled
**docker.service                                enabled**
[root@bi-test systemd]#
```

docker 컨테이너 restart 옵션

no: 기본 옵션입니다. 재시작 하지 않습니다.
always: 컨테이너가 멈추면 즉각 재시작 하고, 수동으로 컨테이너를 종료 할 수 있지만 도커 데몬이 재시작 할 때 다시 켜집니다.
on-failure: 컨테이너에 에러가 발생 한다면 재시작 합니다. 도커데몬 재시작 시에는 자동으로 실행되지 않습니다.
unless-stopped : always 와 비슷 하지만 수동으로 컨테이너를 종료했다면 재시작 하지 않습니다.

```
docker update --restart=unless-stopped elastic
docker update --restart=unless-stopped dutypark-db
docker update --restart=unless-stopped PostgreSQL
docker update --restart=unless-stopped oracle
```

	# 전체 설정 확인
  
docker inspect elastic
```
"RestartPolicy": {
                "Name": "always",
                "MaximumRetryCount": 0
            }
```	    

# RestartPolicy만 확인
docker inspect elastic | grep -A 3 "RestartPolicy"

