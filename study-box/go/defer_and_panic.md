## Defer 와 Panic

### Defer

- 특정 문장 혹은 함수를 나중에(defer를 호출하는 함수가 **리턴하기 직전**에) 실행하게 함.

- 일반적으로 JAVA의 finally블럭처럼 마지막에 Clean-up 작업을 위해 사용.

  ```go
  package main
   
  import "os"
   
  func main() {
      f, err := os.Open("1.txt")
      if err != nil {
          panic(err)
      }
   
      // main 마지막에 파일 close 실행
      defer f.Close()
   
      // 파일 읽기
      bytes := make([]byte, 1024)
      f.Read(bytes)
      println(len(bytes))
  }
  ```

  

### Panic

- **현재 함수를 즉시 멈추고** 현재 함수에 defer함수 들을 모두 실행한 후 즉시 리턴한다.

- 이러한 panic모드 실행 방식은 다시 **상위함수에도 똑같이 적용**되고, 계속 콜스택을 타고 올라가며 적용된다.

  마지막에는 **프로그램이 에러를 내고 종료**한다.



### Recover

- panic함수에 의한 패닉상태를 다시 정상상태로 되돌리는 함수.
