docker pull container-registry.oracle.com/database/express:21.3.0-xe

docker container create    -it    --name oracle    -p 1521:1521    -e ORACLE_PWD=wiseu8    container-registry.oracle.com/database/express:21.3.0-xe
