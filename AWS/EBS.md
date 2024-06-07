# EBS(Elastic Block Store)란 무엇인가?
AMAZON EBS는 AWS 클라우드의 EC2 인스턴스에 사용할 영구 블록 스토리지 볼륨을 제공,
각 EBS 볼륨은 가용 영역 내에 자동으로 복제되어 구성요소 장애로부터 보호해주고 고가용성 및 내구성을 제공한다.
**쉽게 말해 하드디스크라고 생각하면 된다.**

# EBS 용어

## Snapshot
EBS는 현재 저장된 데이터 상태 그대로 보관할 수 있는데, 이를 스냅샷이라고 한다. 미리 만들어진 스냅샷을 선택해서 똑같은 데이터가 저장된 상태로 EBS를 새로 만들 수 있다.

## Volume(볼륨) 
EBS의 가장 기본적인 형태로 OS에서 바로 사용 가능한 형태

## Image(이미지) 
AMI(Amazon Machine Image)의 형태로 OS가 설치된 형태이며, 이를 통해 EC2 인스턴스를 생성함

## IOPS (Input/Output Operation Per Second)
저장 장치의 성능 측정 단위
IOPS의 I/O 단위는 16KB

 
