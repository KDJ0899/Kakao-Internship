## 스위치 (Switch)

- 다른 언어와 다른점은 case의 코드 실행을 마치면 알아서 break가 작동.

  ```go
    switch os := runtime.GOOS; os {
      case "darwin":
          fmt.Println("OS X.")
      case "linux":
          fmt.Println("Linux.")
      default:
  ```

- Fallthrough 

  - 특정 case 문을 실행한뒤 다음 case의 문장을 실행하고 싶을때 사용.

- 스위치에서 조건을 생략하면 "switch ture"와 같습니다.

- 만약 긴 if - then - else를 작성해야 할 때, 이 구조를 사용하면 코드를 깔끔하게 작성 가능.

  ```go
  t := time.Now()
      switch {
      case t.Hour() < 12:
          fmt.Println("Good morning!")
      case t.Hour() < 17:
          fmt.Println("Good afternoon.")
      default:
          fmt.Println("Good evening.")
      }
  ```

