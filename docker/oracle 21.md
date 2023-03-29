## oracle 이미지 불러오기
docker pull container-registry.oracle.com/database/express:21.3.0-xe

## 도커 생성하기
docker container create    -it    --name oracle    -p 1521:1521    -e ORACLE_PWD=wiseu8    container-registry.oracle.com/database/express:21.3.0-xe

## 테이블 스페이스 생성
CREATE TABLESPACE wiseu DATAFILE '/opt/oracle/oradata/XE/wiseu.dbf' SIZE 500M AUTOEXTEND ON NEXT 5M;

## 계정 생성하기
CREATE USER wiseu8 IDENTIFIED BY wiseu8 DEFAULT TABLESPACE wiseu;

## Grant 권한 주기
GRANT CONNECT,resource,dba TO wiseu8;

## 오라클 +docker timezon 변경
실행중인 Docker Container에 bash로 들어갑니다.
```
  $ sudo docker exec -u 0 -it oracle bash
```

 

시스템의 localtime을 아래의 명령어로 변경하고 bash에서 나갑니다.
```
  # cd /etc
  # rm -f localtime
  # ln -s /usr/share/zoneinfo/Asia/Seoul localtime
  # exit
 ```

Docker Container를 재시작합니다.
```
  $ sudo docker restart oracle
```
확인은 sysdate로 합니다. CURRENT_DATE는 client의 시간을 따릅니다.
