## 함수

- 함수의 매개변수의 타입은 변수명 뒤에 명시.
- 마지막 매개변수에만 타입을 명시하고 나머지는 생략 가능.
- 하나의 함수는 여러 개의 결과를 반환 가능.
- 반환 값에 이름을 부여하면 변수처럼 사용가능.
- 함수도 값처럼 사용 가능.

  ```go
  func add(x int, y int) int {
  	return x + y
  }
  ```

### 가변 인자 함수 (Varidic Function)

- 함수에 고정된 수의 파라미터들을 전달하지 않고 다양한 숫자의 파라미터를 전달하고자 할 때 ...을 사용.

  ```go
  func main() {   
      say("This", "is", "a", "book")
      say("Hi")
  }
   
  func say(msg ...string) {
      for _, s := range msg {
          println(s)
      }
  }
  ```

  

### 익명 함수

- 함수명을 갖지 않는 함수.

- 일반적으로 그 함수 전체를 변수에 할당하거나 다른 함수의 파라미터에 직접 정의되어 사용됨.

  ```go
  func main() {
      sum := func(n ...int) int { //익명함수 정의
          s := 0
          for _, i := range n {
              s += i
          }
          return s
      }
  
      result := sum(1, 2, 3, 4, 5) //익명함수 호출
  }
  ```





- GO에서 함수는 일급함수로서 기본 타입과 동일하게 취급. 따라서 다른 함수의 파라미터로 전달하거나 리턴값으로 사용 가능.

  ```go
  func main() {
      //변수 add 에 익명함수 할당
      add := func(i int, j int) int {
          return i + j
      }
   
      // add 함수 전달
      r1 := calc(add, 10, 20)
      println(r1)
   
      // 직접 첫번째 파라미터에 익명함수를 정의함
      r2 := calc(func(x int, y int) int { return x - y }, 10, 20)
      println(r2)
   
  }
   
  func calc(f func(int, int) int, a int, b int) int {
      result := f(a, b)
      return result
  }
  ```



### type문을 사용해 함수 원형 정의

- 자주 사용되는 함수 원형을 정의하여 재사용 할 수 있음.

- 이렇게 함수의 원형을 정의하고 함수를 타 메소드에 전달하고 리턴받는 기능을 타 언어에서는 흔히 델리게이트(Delegate)라 부름.

  ```go
  // 원형 정의
  type calculator func(int, int) int
   
  // calculator 원형 사용
  func calc(f calculator, a int, b int) int {
      result := f(a, b)
      return result
  }
  ```

  



### **클로저** **(Clouser)**

- 클로저는 함수 안에 만들어진 익명 함수로서 익명 함수 외부에 있는 변수까지 접근이 가능한 함수.

- 코드에서 adder함수는 클로져를 반환합니다.

- 각각의 클로저는 자신만의 sum변수를 가집니다.

  ```go
  package main
  
  import "fmt"
  
  func adder() func(int) int {
      sum := 0
    
      return func(x int) int { // 클로저
          sum += x
          return sum
      }
  }
  
  func main() {
      pos, neg := adder(), adder()
    
      for i := 0; i < 10; i++ {
          fmt.Println(
              pos(i),
              neg(-2*i),
          )
      }
  }
  ```

  
