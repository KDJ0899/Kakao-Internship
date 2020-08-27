## 채널 (Channels)

- 참고: [http://golang.site/go/article/22-Go-%EC%B1%84%EB%84%90](http://golang.site/go/article/22-Go-채널)

- 채널은 채널 연산자 <- 를 이용해 값을 주고 받을 수 있는, 타입이 존재하는 파이프입니다.

- 채널은 make() 함수를 통해 미리 생성되어야 하며, 채널 연산자 <-를 통해 데이터를 주고 받음

- 흔히 고루틴 사이 데이터를 주고 받는데 사용하는데 상대편이 준비될 때까지 채널에서 대기함으로써 별도의 lock을 걸지 않고 데이터를 동기화 하는데 사용.

  ```go
  package main
   
  func main() {
    // 정수형 채널을 생성한다 
    ch := make(chan int)
   
    go func() {
      ch <- 123   //채널에 123을 보낸다
    }()
   
    var i int
    i = <- ch  // 채널로부터 123을 받는다
    println(i)
  }
  ```

- 채널은 수신자와 송신자가 서로 기다리는 속성때문에, 이를 이용하여 고루틴이 끝날 때까지 기다리는 기능 구현 가능.

  ```go
  package main
   
  import "fmt"
   
  func main() {
      done := make(chan bool)
      go func() {
          for i := 0; i < 10; i++ {
              fmt.Println(i)
          }
          done <- true
      }()
   
      // 위의 Go루틴이 끝날 때까지 대기
      <-done
  }
  ```



### Go 채널 버퍼링

- Go채널은 2가지 채널이 있는데, Unbuffered Channel 과 Buffered Channel이 있다. 위의 예제에서의 채널은 Unbuffered Channel로서 이 채널에서는 하나의 수긴자가 데이터를 받을 때 까지 송신자가 데이터를 보내는 채널에 묶여 있게 된다.

- 하지만, Buffered Channel을 사용하면 비록 수신자가 받을 준비가 되어 있지 않을지다로 지정된 버퍼만큼 데이터를 보내고 계속 다른 일을 수행할 수 있다.

- 버퍼 채널은 make(chan type, N)함수를 통해 생성, N에 사용할 버퍼 갯수를 넣는다.

- 버퍼 채널을 이용하지 않는 경우, 아래와 같은 코드는 에러를 발생시킴. 왜냐하면 메인루틴에서 채널에 1을 보내면서 상대편 수신자를 기다리고 있는데, 이 채널을 박는 수신자 Go루틴이 없기 때문

  ```go
  package main
   
  import "fmt"
   
  func main() {
    c := make(chan int)
    c <- 1   //수신루틴이 없으므로 데드락 
    fmt.Println(<-c) //코멘트해도 데드락 (별도의 Go루틴없기 때문)
  }
  ```

- 하지만 아래와 같이 버퍼채널을 사용하면, 수신자가 당장 없더라도 최대버퍼 수까지 데이터를 보낼 수 있음.

  ```go
  package main
   
  import "fmt"
   
  func main() {
      ch := make(chan int, 1)
   
      //수신자가 없더라도 보낼 수 있다.
      ch <- 101
   
      fmt.Println(<-ch)
  }
  ```



### 채널 파라미터

- 채널을 함수의 파라미터로 전달할 때, 일반적으로 송수신을 모두 하는 채널을 전달하지만, 특별히 해당 채널로 송신 혹은 수신만 할지 지정할 수 있다.

- 송신 파라미터는 (p chan<-int), 수신 파라미터는 (p <- chan int)와 같이 사용.

  ```go
  package main
   
  import "fmt"
   
  func main() {
      ch := make(chan string, 1)
      sendChan(ch)
      receiveChan(ch)
  }
   
  func sendChan(ch chan<- string) {
      ch <- "Data"
      // x := <-ch // 에러발생
  }
   
  func receiveChan(ch <-chan string) {
      data := <-ch
      fmt.Println(data)
  }
  ```



### 채널 닫기

- 채널을 오픈한 후 데이터를 송신한 후, close()함수를 사용하여 채널을 닫을 수 있다.

- 채널을 닫게 되면, 해당 채널로는 더이상 송신을 할 수 없지만, 채널이 닫힌 이후에도 계속 수신은 가능.

  ```go
  package main
   
  func main() {
      ch := make(chan int, 2)
       
      // 채널에 송신
      ch <- 1
      ch <- 2
       
      // 채널을 닫는다
      close(ch)
   
      // 채널 수신
      println(<-ch)
      println(<-ch)
       
      if _, success := <-ch; !success {
          println("더이상 데이타 없음.")
      }
  }
  ```

  

### 채널 Range문

- 채널에서 송신자가 송신을 한 후, 채널을 닫을수 있고, 수신자는 **임의의 갯수**의 데이터를 채널이 닫힐 때까지 **계속 수신**할 수 있다.

  ```go
  for i := range ch {
          println(i)
      }
  ```

  

### 채널 Select문

- Select문은 **복수 채널들을 기다리면서** 준비된 채널을 실행하는 기능. 

- 즉, 여러개의 case문에서 각각 다른 채널을 기다리다가 준비된 채널 case를 실행하는 것.

- 만약 복수 채널에 신호가 오면, **Go 런타임이 랜덤하게** 그 중 한개를 선택함.

- 하지만, default문이 있으면, case문 채널이 준비되지 않더라도 계속 대기하지 않고 **바로 default문을 실행**한다.

  ```go
  package main
   
  import "time"
   
  func main() {
      done1 := make(chan bool)
      done2 := make(chan bool)
   
      go run1(done1)
      go run2(done2)
   
  EXIT:
      for {
          select {
          case <-done1:
              println("run1 완료")
   
          case <-done2:
              println("run2 완료")
              break EXIT
          }
      }
  }
   
  func run1(done chan bool) {
      time.Sleep(1 * time.Second)
      done <- true
  }
   
  func run2(done chan bool) {
      time.Sleep(2 * time.Second)
      done <- true
  }
  ```

  



