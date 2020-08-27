## 에러 (Error)

- 참고: [https://kamang-it.tistory.com/entry/Go17%EC%97%90%EB%9F%ACError%EC%B2%98%EB%A6%AC](https://kamang-it.tistory.com/entry/Go17에러Error처리)

- 에러 문장으로 자신을 표현할 수 있는 것은 모두 에러.

- 에러와 예외의 결정적인 차이점은 회피할수 있냐 아니냐로 구분.

- go에서는 errorfmf 함께 반환함.

  ```go
  func div(num1 float32, num2 float32) (float32, error) {
     if (num2 != 0) {
        return num1 / num2, nil
     } else {
        return 0, &MyError{time.Now(), "You can't divide by zero."}
     }
  }
  ```

- 연습 예제

  ```go
  package main
  
  import (
      "fmt"
  )
  
  type ErrNegativeSqrt float64
  
  func (e ErrNegativeSqrt) Error() error{
      if(e<0){
          return fmt.Errorf("cannot Sqrt negative number: %f", e)
      }
      return nil
  }
  
  func Sqrt(f float64) (float64, error) {
      e := ErrNegativeSqrt(f)
      error := e.Error()
      return 0, error
  }
  
  func main() {
      fmt.Println(Sqrt(2))
      fmt.Println(Sqrt(-2))
  }
  
  ```

