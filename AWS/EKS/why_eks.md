## 왜 AWS EKS를 사용할까?

*EKS(Elastic Kubernetes Service)
: AWS에서 Kubernetes라는 도구를 쉽게 관리할 수 있도록 도와주는 서비스

e.g.) 여러 개의 애플리케이션을 다양한 서버에서 운영할 때, EKS는 이를 분배/관리

---
### 구조
- nginx를 실행 시, nginx를 포함한 container의 pod 생성 
- Self healing 기능이 존재하지만, pod 생성된다고 해서 Kubernetes가 자동적으로 실행되지 X
- ReplicaSet: pod가 잘 작동하고 있고, 개수를 잘 유지하는지 감시하는 역할
- Deployment: 어떤 전략으로 배포하고 문제가 생기면 어떻게 관리할 것인지

---
### `run`명령을 내렸을 때, 내부에서 발생하는 일 

- 크게 `Master Node`, `Worker Node`로 나뉨
- API 서버, Controller Manager, etcd, Scheduler, Kublet, Kube proxy 와 같은 `Components`가 존재
- 각 Components는 `Watch` 기능을 작동함 = 서로의 변경사항을 감시/감지하고 자신을 감시하는 대상에게는 `notify`를 보냄
