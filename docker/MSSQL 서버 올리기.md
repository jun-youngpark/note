# mssql 서버 올리기.

1. docker mssql 이미지 다운로드 하기
``` docker pull mcr.microsoft.com/mssql/server:2022-latest ```

2. docker 계정설정하기
``` 
   sudo docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<Mnwise4210#>" \
   -p 1433:1433 --name wiseu --hostname wiseu \
   -e 'TZ=Asia/Seoul' \
   -d \
   mcr.microsoft.com/mssql/server:2022-latest
   ```
결과값 95985897e9e1b0b2a37e31572836f235d2ced611bb308f6defe17837bc9855e8

   ![image](https://user-images.githubusercontent.com/54339804/209776157-14c9a886-28ac-467b-9e71-d6802d18e587.png)

3. 확인하기
 ``` sudo docker ps -a ```
 
4. 명령을 사용하여 실행 중인 컨테이너 내에서 대화형 bash 셸을 시작합니다. 
다음 예에서 mssql은 컨테이너를 만들 때 --name 매개 변수가 지정한 이름입니다. 

```   - docker exec -it mssql bash ```

 

7. 컨테이너 내부로 들어가면 sqlcmd를 사용하여 로컬로 연결합니다. 
Sqlcmd는 기본적으로 경로에 있지 않으므로 전체 경로를 지정해야 합니다

  ```- /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P 'mnwise@4210#' ```

  mssql 생성 및 접근 완료
