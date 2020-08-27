## 컨텍스트 (Context)

- https://jaehue.github.io/post/how-to-use-golang-context/

- 사전적 의미로 **맥락을 유지하는 통로**

- 컨텍스트를 사용하는 일반적인 패턴은 현재 맥락안에서 유지해야 할 값을 컨텍스트에 담아서 전달하고, 

  필요한 곳에서 컨텍스트의 값을 꺼내 사용하는 것.

- 컨텍스트의 값을 꺼내 사용할때 주의해야 할 점.

  - 컨텍스트의 Value 메소드의 리턴값은 interface{} 타입이고, 컨텍스트에 값이 존재하지 않는 경우 nil이 리턴된다.

- 개발자는 context를 이용해서 패키지 전체에서 함수 인터페이스를 일관되게 유지 할 수 있다. 

  이를 위해서는 컨텍스트를 구조체 안에 저장하지 않아야 한다. 대신 명시적으로 전달을 해야 한다. 

  보통은 **ctx** 라는 이름으로 함수의 첫번째 매개 변수로 전달 한다.


### Cancelation

- 고루틴을 사용할 때 주의해야 할 점은 내가 실행한 고루틴이 일정 시간 안에 반드시 종료될 것이란 것을 보장해야함.

- 컨텍스트의 Cancelation 기능을 사용하면 고루틴의 생명주기를 쉽게 제어할 수 있음.

  ```go
  ctx, cancel := context.WithCancel(context.Background())
  
  go func() {
  	// 고루틴을 종료해야 할 상황이 되면 cancel 함수 실행
  	cancel()
  }()
  
  result, err := longFuncWithCtx(ctx)
  ```



### Timeout & Deadline

- WithDeadline - 해당 시각에 취소신호가 전달. (Deadline 메소드를 사용하면 남은 시간을 확인할 수 있음.)
- WithTimeout - 해당 시간이 지나면 취소신호가 전달.

```go
ctx, cancel := context.WithTimeout(context.Background(), maxDuration)

go func() {
	// 고루틴을 종료해야 할 상황이 되면 cancel 함수 실행
	cancel()
}()

start := time.Now()
result, err := longFuncWithCtx(ctx)
fmt.Printf("duration:%v result:%s\n", time.Since(start), result)
```

