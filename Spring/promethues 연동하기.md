# Prometheus란?

## 현재 Kubernetes 상에서 가장 많이 사용하는 오픈 소스 기반 모니터링 시스템이다.

# Prometheus Architecture
##  Prometheus는 Pull 방식을 사용하여, 서버에 클라이언트가 떠 있으면 서버가 주기적으로 클라이언트에 접속해서 데이터를 가져오는 방식을 취한다.

# Spring boot와의 연동방법
### spring boot에서는 이미 promethues 연동을 위한 플러그인이 존재하므로, 라이브러리 의존성 추가만 해주면 끝난다!


* pom.xml에 다음과 같이 설정한다.
```
	<!-- 프로메테우스 연동-->
		<dependency>
			<groupId>io.micrometer</groupId>
			<artifactId>micrometer-registry-prometheus</artifactId>
		</dependency>
   
```
* application.yml에 다음과 같이 설정한다.
```
management:
  endpoints:
    metrics:
      enabled: true
    prometheus:
      enabled: true
```


* 프로메테우스를 공식 홈페이지에서 다운로드후 실행하면 아래와 같다

![image](https://user-images.githubusercontent.com/54339804/188322621-c0f96ced-5737-4f19-9bff-8f3bad2d6c5a.png)

* 프로메테우스에서 target 설정은 prometheus.yml 에서 Spring boot 서버의 타겟을 설정한다.
	static_configs:
      		- targets: ["localhost:8080"]
      	metrics_path: '/actuator/prometheus' 
      
* 프로메테우스 실행 후 기본 port는 9090이다.

잘 연결되었는지 확인 하는 방법!

![image](https://user-images.githubusercontent.com/54339804/188322549-0932e521-5af6-4c93-9a1f-37d421363af9.png)



먼저 서버에 reqeust를 요청해보고 (/city/get/1) 프로메테우스에서 요청 시간에 대한 값을 수집함을 확인한다.

![image](https://user-images.githubusercontent.com/54339804/188322517-a2f7452a-9323-43a5-9de9-6f79bc125aac.png)
 
 
 # E N D ! ! 간편하다.


