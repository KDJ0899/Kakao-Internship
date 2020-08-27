## 컨트롤러 (Controller)

- 컨트롤러는 기본 오브젝트들을 생성하고 이를 관리하는 역할을 함.



### Replication Controller

- Pod를 관리해주는 역할. 지정된 숫자를 Pod를 기동시키고, 관리하는 역할.
  - Selector : 먼저 Pod selector는 라벨을 기반으로 하여, RC가 관리한 Pod를 가지고 오는데 사용.
  - Replica 수: RC에 의해서 관리하는 Pod의 수인데, 그 숫자만큼 Pod의 수를 유지하도록 함.
  - Pod를 추가로 기동할 때 어떻게 Pod를 만들지 Pod의 정보에 대해 필요한데, 이는 Pod Template에 정의함.

### Deployment

- Replication controller와 Replica Set의 좀더 상위 추상화 개념.



### DaemonSet

- Pod가 각각의 노드에서 하나씩만 돌게 함. (균등하게 배포)
- 보통 서버 모니터링이나 로그 수집용도.
- 모든 노드가 아닌 특정 노드들만 선택할수도 있음.



### Job

- 한번 실행되고 끝나는 Pod를 관리.
- Job 컨트롤러가 종료되면 Pod도 같이 종료됨.
- 컨테이너에서 Job을 수행하기 위한 별도의 command를 준다.
- Job command의 성공 여부를 받아 재실행 또는 종료여부를 결정.



### CronJob

- 주기적으로 돌아야하는 Pod를 관리.
- 별도의 Schedule을 정의해야 함.



### Stateful

- DB와 같이 상태를 가지는 Pod를 관리.



