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


- EKS는 `Master Node`에서 일어나는 복잡한 과정을 자동적으로 관리해줌
- `Worker Node`에서 일어나는 과정도 EKS Node Groups로 관리 가능

---
## Docker vs Kubernetes
`Docker`는 적은 컨테이너를 다루는 데에 특화

`docker compose`를 사용하면 되지만 test할 때마다 입력해야 하는 명령값이 많다.

e.g.) Repick 프로젝트에서 개발을 할 때도, Infra가 지원되지 전까지는 docker compose를 활용했는데, docker 빌드를 할 때마다 연결된 서버나 front측에서 docker를 rebuild해야 해서 매번 지우고 다시 compose up 했다. 이와 같은 번거로움이 존재한다.

---
`Kubernetes`를 사용하면 `kubectl`응 이용해서 다수의 컨테이너 관리가 용이

local에서 Kubernetes를 사용하는 방법을 사용할 수도 있겠지만, Repick 프로젝트에서 봤듯이 EKS에 올리지 않으면 모든 Node를 관리해줘야 한다.
하지만 EKS에 올린 경우, 앞서 말했던 것처럼 `Master Node`는 아마존에서 관리 + `Worker Node`는 사용자가 관리하면 되니까 개발자의 개발 비용이 줄어듦