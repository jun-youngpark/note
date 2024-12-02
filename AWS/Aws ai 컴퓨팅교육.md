# AWS Compute & Security

## EC2 개요
* 인스턴스 기동 시에만 데이터 보존
* 스냅샷 지원 X

# EBS
* 영구 스토리지
* 스냅샷 지원 O

## EC2 인스턴스 유형
* 카테고리 (범용,버스팅 가능,컴퓨팅 집약접,스토리지 등등)
* 기능 (프로세서 AWS Gravtion,Intel 등등), 빠른프로세서 ,메모리공간 , 베어 메탈

## ECS 인스턴스 선택
* 카테고리 +
* C7gn.xlarage
* c7(인스턴스 세대) , gn(추가기능) , xlarge (인스턴스 크기)
* 조언받기 기능
* 최적화 기능

## 컴퓨팅 관련 기능 및 서비스
### ELB - 로드밸런서 (트래픽 분산) , 트래픽에 따라 자동 조정
* L4/L7 - L4가 미세하게나마 성능이 좋음
* L4는 IP,PORT 정보만 가지고 파악
* L7은 HTTP 헤더등 APP 

### Auto Scaling 
* Fleet Managemnet - 비정상 인스턴스 교체 (장애시)
* Dynymic Scaling - 수요에 맞게 확장 (Cpu 사용률,로드밸런서 트래픽 등을 보고)

### Lunch Template
* 시작을 간소화 하기 위해 시작 요청을 템플릿화(시작파라미터,인스턴스타입,EBS,AMI,NetWork Interface)

### Instance Conect 
* 브라우저 콘솔

## AWS IAM
USER
USEGROUP
ROLE
Policy

Assum - 
