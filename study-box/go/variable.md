## **변수**

- 변수 선언은 var, 함수의 매개변수처럼 타입은 문장 끝에 명시.

- 변수 선언과 함께 변수 각각을 초기화 가능. 초기화하는 경우 타입 생략 가능.

- 함수 내에서 := 을 사용하면 var과 명시적인 타입을 생략할 수 있음.

- = 대입, := 변수 선언 및 대입.

  ```go
  c, python, java := true, false, "no!"
  ```

  

- 상수는 const키워드와 함께 변수처럼 선언, character, string, boolean, 숫자타입중의 하나.

- 숫자형 상수는 정밀한 값 표현 가능. 

  ```go
  import "fmt"
  
  const (
      Big   = 1 << 100
      Small = Big >> 99
  )
  
  func needInt(x int) int { return x*10 + 1 }
  func needFloat(x float64) float64 {
      return x * 0.1
  }
  
  func main() {
      fmt.Println(needInt(Small))
      fmt.Println(needFloat(Small))
      fmt.Println(needFloat(Big))
  }
  ```

