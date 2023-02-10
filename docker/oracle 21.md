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
