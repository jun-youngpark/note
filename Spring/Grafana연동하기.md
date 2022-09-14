## Grafana 란?
*  데이터를 대시보드 형태로 제공해주는 시각화 툴!

# Spring Boot 와 Grafana 연동하기

먼저 Granafa 설치필요! 

Grafana를 설치하기 위한 자세한 정보는 아래 링크를 통해 확인할 수 있다.

* 윈도우버전

[The Grafana backend has a number of configuration options defined in its config file (usually located at…
grafana.com](https://grafana.com/grafana/download?platform=linux)
 

* Red Hat, CentOS, RHEL, and Fedora(64 Bit) 계열의 리눅스 환경에서 설치버전

  먼저 공식 문서에서 제공하는 것 처럼 아래 명령어를 실행한다.

$ wget https://dl.grafana.com/oss/release/grafana-6.7.2-1.x86_64.rpm $ sudo yum install grafana-6.7.2-1.x86_64.rpm


* 실행 후 http://localhost:3000 에 접속해보자. 다음과 같이 Grafana login 화면을 볼 수 있다.
기본  ID/PW인 admin/admin 

1. Granafa에서 프로메테우스 설정하기
 ![image](https://user-images.githubusercontent.com/54339804/190165295-aa347b5e-d20a-4e9a-beda-3556c6264c8f.png)
2. Datasoure 에서 add data source 프로메테우스 추가하기
![image](https://user-images.githubusercontent.com/54339804/190165483-b3055823-d9cb-4a7b-bfde-449aa2d6c7ca.png)
3. URL 부분에 프로메테우스 URL 설정 후 SAVE&TEST로 연결 확인!
![image](https://user-images.githubusercontent.com/54339804/190166190-656d5281-d393-43df-8e86-9ad0ce16e21e.png)

4. 원하는 값 모니터링하기 (add panel 버튼 클릭후 커스텀하기!)
![image](https://user-images.githubusercontent.com/54339804/190169539-a709f831-4001-466a-98fe-ac42e5798bb1.png)
* request 요청수에 대한 커스터마이징 성공

