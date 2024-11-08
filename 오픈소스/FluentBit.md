# fluent-bit이란
일반적으로 로깅은 Elastic search, LogStatsh, Kibana의 앞자리를 가져온 ELK 스택이 많이 사용됩니다.  
그러나  k8s 클러스터 환경에서는 로그를 수집하는 역할을 하는 'L'의 LogStatsh 대신 fluent bit 이라는 로그 수집기를 사용하는 경우도 많습니다(EFK라고 불립니다)
fluent bit은 대표적인 로그 수집기중(LogStash, fluentd, fluentbit) 가장 가볍고(다른 수집기에 비해 10배이상 가볍습니다), 분산한경을 고려하여 만들어졌기에 최근 k8s의 로그 수집기로 각광받고 있습니다.

#  EFK 아키텍쳐

![image](https://github.com/user-attachments/assets/d64c3164-261b-4701-abc8-be926912efd6)


# Fluent Bit의 작동 방식 예시
입력(수집): 파일, 컨테이너, 네트워크 등으로부터 로그를 수집합니다.
필터링: 수집된 로그에서 필요한 정보만을 남기거나 불필요한 데이터를 제거합니다.
출력(전송): 최종적으로 필터링된 로그를 설정된 출력 대상으로 전송합니다. 예를 들어, Elasticsearch와 같은 데이터 저장소에 보내거나, 모니터링 툴과 연결해 실시간 분석이 가능하도록 전송합니다.

과정 도식화
먼저 각 노드마다 데몬셋 형태로 fluentbit가 배포되고 각 노드의 hostpath를 통해서 fluentbit가 로그를 쪽쪽 빨아먹는다. (수집한다)
![image](https://github.com/user-attachments/assets/debe8356-a9e2-4834-add6-b9d8a261f721)


이렇게 수집된 로그들은 Output으로 정의된 Amazon CloudWatch의 각 로그 그룹으로 로그를 전송한다.

![image](https://github.com/user-attachments/assets/7740c1c3-6f60-4feb-ad01-809f8b275e5b)


이처럼 fluntbit🐦 통해서 중앙집중형 로깅 시스템을 구축할 수 있다.
