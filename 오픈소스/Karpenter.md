# Karpenter
# Karpenter는 ?
AWS에서 개발한 Kubernetes 클러스터의 자동화된 노드 프로비저닝 도구입니다.
Karpenter는 Kubernetes 워크로드의 요구 사항에 따라 동적으로 EC2 인스턴스를 생성하고 관리하여 클러스터 내의 리소스를 효율적으로 사용할 수 있게 합니다. 
주로 클러스터의 오토스케일링을 간편하게 하여 비용 최적화와 성능 향상을 지원합니다.


 
# CAS(Cluster AutoScaler) vs Karpenter 비교 
Karpenter와 Kubernetes의 기본 Cluster Autoscaler는 비슷한 기능을 하지만, Karpenter는 Cluster Autoscaler보다 더 빠르고 유연한 확장성을 제공합니다.

빠른 리소스 프로비저닝: Karpenter는 클러스터의 상태를 실시간으로 모니터링하고 필요한 리소스를 즉시 제공하여, 더 빠르게 확장과 축소를 수행합니다.
유연한 리소스 관리: Karpenter는 다양한 인스턴스 유형을 선택할 수 있고, 더 세밀한 리소스 조정을 통해 최적의 비용 효율성을 제공합니다.
Karpenter는 AWS 환경에서 Kubernetes를 사용하는 경우 특히 유용하며, 클라우드 리소스를 최적화하면서도 자동화된 리소스 관리를 원하는 기업에게 적합한 도구입니다.

Cluster Autoscaler는 **구글(Google)**이 Kubernetes의 일부로 개발한 오픈 소스 프로젝트로, Kubernetes 클러스터의 자동 확장(오토스케일링)을 지원하는 도구입니다.
이 도구는 사용자가 설정한 노드 그룹을 기반으로, 클러스터의 자원 부족 상태를 감지하고 필요한 리소스를 자동으로 추가하여 Kubernetes 워크로드가 원활히 실행될 수 있도록 합니다.
