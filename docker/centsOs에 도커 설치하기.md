# centsOs에 도커 설치하기


*  CentOS 7 에 docker 설치 (https://docs.docker.com/engine/install/centos/)


 
1. 서버에 Docker 리포지토리 설정
저장소를 사용하여 설치 
유틸리티 yum-utils를 제공하는 패키지를 설치 하고 리포지토리를 설정합니다.yum-config-manager
```sudo yum install -y yum-utils
 sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
``` 
2. 도커 엔진 설치
최신 버전 의 Docker Engine, containerd 및 Docker Compose를 설치 하거나 다음 단계로 이동하여 특정 버전을 설치합니다.
``` sudo yum install docker-ce docker-ce-cli containerd.io docker-compose-plugin ```

GPG 키를 수락하라는 메시지가 표시되면 지문이 일치하는지 확인하고 맞으면 060A 61C5 1B55 8A7F 742B 77AA C52F EB6B 621E 9F35수락합니다.
이 명령은 Docker를 설치하지만 Docker를 시작하지는 않습니다. 또한 docker그룹을 생성하지만 기본적으로 그룹에 사용자를 추가하지는 않습니다.
 
 
