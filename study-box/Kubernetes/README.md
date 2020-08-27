# Kubernetes


## Contents


- **[Kubernetes](https://github.com/KDJ0899/Kakao-Internship/tree/master/study-box/Kubernetes/README.md#kubernetes-1)**
- **[오브젝트 (Object)](https://github.com/KDJ0899/Kakao-Internship/tree/master/study-box/Kubernetes/Object.md#%EC%98%A4%EB%B8%8C%EC%A0%9D%ED%8A%B8-object
)**
  - Pod
  - Volume
  - Service
  - NameSpace
  - 라벨 (Label)
  - 라벨 셀렉터 (Label Selector)
- **[컨트롤러](https://github.com/KDJ0899/Kakao-Internship/tree/master/study-box/Kubernetes/Controller.md#%EC%BB%A8%ED%8A%B8%EB%A1%A4%EB%9F%AC-controller)**
  - Replication Controller
  - Deployment
  - DaemonSet
  - Job
  - CronJob
  - Stateful
- **[Kubectl](https://github.com/KDJ0899/Kakao-Internship/tree/master/study-box/Kubernetes/kubectl.md#kubectl)**
  - Kubectl 문법


### Kubernetes

쿠버네티스 클러스터는 크게 두 종류의 서버로 구성됨.

- 클러스터를 관리하는 **마스터**

  - 노드들의 상태를 **관리하며 제어**, 1대만 구성할 수 있으나 고가용성 서비스라면 3대 이상으로 구성장애가 발생하면 남은 서버중 한대가 마스터의 역할을 함.

  - Kube-Scheduler : 클러스터 내에서 발생하는 파드의 **생성**에 대한 노드의 **자원 할당**을 선택하는 컴포넌트. 

    정해놓은 조건에 맞게 빈 노드에 파드를 할당.

  - Kube-Controller-Manager : 토드 컨트롤러외에 아래의 다수의 컨트롤러를 **복잡성을 줄이기 위해서** 하나로 구성한 컴포넌트.

    - 노드 컨트롤러 : 노드의 중지에 대한 대응
    - 레플리케이션 컨트롤러 : 전체 레플리케이션 컨트롤러 객체에 대한 파드 숫자 유지
    - 엔드포인트 컨트롤러 : 서비스와 파드 연결
    - 서비스 어카운트 & 토큰 컨트롤러 : 신규 Name Space에 대한 기본적인 관리

  - Cloud-Controller-Manager : 클라우드 사업자와 컨트롤러들을 연결하여 관리하는 역할을 함.

    - 노드 컨트롤러 : 노드 중지이후 클라우드 상에서 **삭제되었는지 판별**하기 위함.
    - 라우트 컨트롤러 : 클라우드 서비스상의 네트워크 라우팅 관리
    - 서비스 컨트롤러 : 클라우드 제공사업자 서비스의 로드밸런서를 생성, 업데이트 삭제
    - 볼륨 컨트롤러 : 클라우드 서비스상의 볼륨을 노드와 연결하거나 마운트

  - Kube-apiserver : 쿠버네티스상에서 이루어지는 모든 요청은 이를 통해서 각 컴포넌트에 전달되고 실행된다.

    **외부에서 클라우드를 관리할 수 있는 핵심 API**, 수평 확장이 가능하므로 요청이 많은 경우 확장할 수 있다.

  - etcd : key - value 저장소로서 모든 클러스터의 데이터를 저장하는 저장소.

    

- 실제 컨테이너를 실행시키는 **노드**

  - 마스터 노드의 명령을 받아 사용자가 선언한 Pod나 Job을 실행함, 실제 docker컨테이너가 동작하는 것은 노드에서 동작함.

  - Kebelet : 프로세스로서 실행 가능하며 도커를 관리한다. Kube - apiserver와 통신하면서 **파드의 생성, 관리, 삭제**를 담당함.

  - Kube - proxy : 개별 노드에서 실행되는 네트워크 프록시로서 파드가 외부와 통신할 수 있게 해주는 등 **네트워크 규칙을 관리.**

  - 컨테이너 런타임 : 클러스터에서 컨테이너의 실행을 담당하는 것으로서 대표적으로 Docker가 있으며,

    Containerd와 같은 다른 런타임도 지원합니다. CRI(Container Runtime Interface)를 만족하는 모든 소프트웨어를 지원.

  

쿠버네트스는 크게 **오브젝트**와 오브젝트를 관리하는 **컨트롤러**로 나눕니다.

사용자는 템플릿 등으로 쿠버네티스에 자원의 '**바라는 상태**'를 정의하고 **컨트롤러**는 바라는 상태와 현재 상태가 일치하도록 **오브젝트를 생성/삭제함.**
