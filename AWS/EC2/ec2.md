## EC2
: Elastic Container Service, 완전관리형 서비스, Docker based

- 장점
    - 기존의 aws 서비스를 결합해 컨테이너 배포에 맞도록 서비스를 만들기 때문에 손쉬운 배포/운영 가능
    - eks 대비 서버 구조 쉬움
    - 클러스터 관리에 대한 추가 비용 X
    - auto scaling, 자동 복구 등 기능 사용 가능
    - 다른 aws 서비스와의 연동성 good

- 단점
    - ec2 인스턴스 직접 관리
        - 보안 패치 등을 직접 처리

---

### 내부 구성
#### 1. Cluster
: 여러 컨테이너의 하드웨어 리소스 그룹화, 컨테이너 라이프사이클 관리
#### 2. Task
: VM에 어떻게 컨테이너를 배포할 것인지
#### 3. Service
: Auto-scaling 등 컨테이너 어떻게 배포/실행/관리할지 task보다 advanced한 설정 내용 포함
