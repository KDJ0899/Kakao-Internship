# GO Lang 

[A Tour of Go]( https://tour.golang.org/) 정리 자료. 

### 유용한 자료

- **[GO Packages](https://golang.org/pkg/)**
- **[Select 다양한 패턴](https://okky.kr/article/547449)**
- **[예제로 배우는 Go 프로그래밍](http://golang.site/Go/Basics)**
- **[가장 빨리 만나는 Go 언어](http://pyrasis.com/go.html)**

### Go Library

- **[zerolog](https://github.com/rs/zerolog)**
  
  Golang으로 할당하지 않고 빠르게 json로그를 남길 수 있는 라이브러리.
- **[viper](https://github.com/spf13/viper)**

- **[chi](https://github.com/go-chi/chi)**
	REST API 서버를 만드는 라이브러리.

- **[Holster](https://github.com/mailgun/holster)**

- **[Swagger](https://github.com/go-swagger/go-swagger)**

## Contents
- **[Go 주요 특징](https://github.daumkakao.com/joel-kim/study-box/tree/master/go#go-%EC%A3%BC%EC%9A%94-%ED%8A%B9%EC%A7%95)**
- **[패키지 (Package)](https://github.daumkakao.com/joel-kim/study-box/blob/master/go/package.md)**
  - Main Package
  - init 함수와 alias
- **[함수 (Function)](https://github.daumkakao.com/joel-kim/study-box/blob/master/go/function.md)**
  - 가변 인자 함수
  - 익명 함수
  - type문을 사용해 함수 원형 정의
  - 클로저 (Clouser)
- **[변수 (Variable)](https://github.daumkakao.com/joel-kim/study-box/blob/master/go/variable.md)**
- **[반복문 (Loop) - for](https://github.daumkakao.com/joel-kim/study-box/blob/master/go/loop.md)**
- **[조건문 (Condition) - if](https://github.daumkakao.com/joel-kim/study-box/blob/master/go/condition.md)**
- **[자료형 (Data Type)](https://github.daumkakao.com/joel-kim/study-box/blob/master/go/data_type.md)**
  - 기본 자료형
  - 문자열 
  - 형변환
- **[구조체 (Struct)](https://github.daumkakao.com/joel-kim/study-box/blob/master/go/struct.md)**
  - 구조체 리터럴
  - new 함수
  - 임베딩(Embedding)
  - 포인터 (Pointer)
- **[슬라이스 (Slice)](https://github.daumkakao.com/joel-kim/study-box/blob/master/go/slice.md)**
- **[맵 (Map)](https://github.daumkakao.com/joel-kim/study-box/blob/master/go/map.md)**
- **[레인지 (Range)](https://github.daumkakao.com/joel-kim/study-box/blob/master/go/range.md)**
- **[스위치 (Switch)](https://github.daumkakao.com/joel-kim/study-box/blob/master/go/switch.md)**
- **[메소드 (Method)](https://github.daumkakao.com/joel-kim/study-box/blob/master/go/method.md)**
  - 포인터 리시버
- **[인터페이스 (Interface)](https://github.daumkakao.com/joel-kim/study-box/blob/master/go/interface.md)**
  - 덕 타이핑(Duck Typing)
  - 빈 인터페이스 사용하기
- **[에러 (Error)](https://github.daumkakao.com/joel-kim/study-box/blob/master/go/error.md)**
- **[웹서버 (HTTP)](https://github.daumkakao.com/joel-kim/study-box/blob/master/go/HTTP.md#%EC%9B%B9%EC%84%9C%EB%B2%84-http)**
  - Http.Handler 인터페이스
  - Http.HandelFunc
  - ServeMux
- **[고루틴 (GoRoutine)](https://github.daumkakao.com/joel-kim/study-box/blob/master/go/go_routine.md)**
- **[채널 (Channel)](https://github.daumkakao.com/joel-kim/study-box/blob/master/go/channel.md)**
  - Go 채널 버퍼링
  - 채널 닫기
  - 채널 닫기 
  - 채널 Range문
  - 채널 Select문
- **[동기화 객체](https://github.daumkakao.com/joel-kim/study-box/blob/master/go/sync_object.md)**
- **[Defer & Panic](https://github.daumkakao.com/joel-kim/study-box/blob/master/go/defer_and_panic.md)**
  - Defer
  - Panic
  - Recover
- **[컨텍스트 (Context)](https://github.daumkakao.com/joel-kim/study-box/blob/master/go/context.md#%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8-context)**
  - Cancelation
  - Timeout & Deadline
  
  
  ## Go 주요 특징

- **정적 타입, 강 타입**

  C/C++, Java와 같이 Compile Time에 Type결정이 이루어지며, 코드 내에서 **암시적 형변환**이 일어나지 않는다.

- **컴파일 언어**

  별도의 Runtime환경이 필요없어 실행 환경이 복잡하지 않음.

- **가비지 컬렉션**

  실행파일 내에 Garbage Collector가 탑재 됨.

- **병행성(Concurrency)**

  Multi Thread, Multi Core에 Go Routine이라는 단위의 함수실행을 한 Thread나 Core별로 동시에 실행시킬 수 있음.

  Thread와 Go Routinedms 1:N관계를 이룰 수 있다.

- **멀티코어 환경 지원**

  Go Routine간에 채널을 통해 통신하여 **데이터를 공유하고 실핼 순서를 제어**할 수 있다. 

- 모듈화 및 패키지 시스템npm, pip, gem 이나 Maven과 같은 **모듈 의존성에 따른 패키지 관리를 언어 차원에서 지원**. 인터넷 상의 패키지들을 바로 가져올 수 있다. import 키워드만 있으면 되며, go get 이나 go install 명령으로 자동으로 패키지들을 가져온다.

  ```go
  import "github.com/kylelemons/go-gypsy/yaml"
               ^         ^          ^     ^
               |         |          |     `-- Package name
               |         |          `-------- Project name
               |         `------------------- Author's handle
               `----------------------------- Hosting site
  ```

- **빠른 컴파일 속도**

  C와 달리 헤더파일이 없고 소스코드를 패키지화 하므로 변결 시 패키지만 재 컴파일 함. 

  문법도 최대한 단순화 하여 컴파일 속도도 빠르고 생산성이 좋음.

  
  
