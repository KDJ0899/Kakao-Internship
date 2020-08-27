## 메소드 (Methods)

- 객체에 연결된 함수, 즉 함수이긴 한데 객체에 연결되어야 메소드라고 부름.

- 고에는 클래스가 없습니다. 하지만 메소드를 구조체(struct)에 붙일 수 있습니다.

- 메소드 리시버는 func키워드와 메소드의 이름 사이에 인자로 들어감.

  ```go
  type Point struct {
     X,Y int
  }
  
  func (p Point) printInfo() {
     fmt.Println(p)
  }
  
  func main()  {
     p := Point{3,4}
     p.printInfo()
  }
  ```

  

- 메소드는 구조체뿐 아니라 아무 타입에나 붙일 수 있다.

- 단, 다른패키지에 있는 타입이나 기본 타입들에 메소드를 붙이는 것은 불가능.

  ```go
  type MyFloat float64
  
  func (f MyFloat) Abs() float64 {
      if f < 0 {
          return float64(-f)
      }
      return float64(f)
  }
  
  func main() {
      f := MyFloat(-math.Sqrt2)
      fmt.Println(f.Abs())
  }
  ```

### 포인터 리시버

- 포인터 리시버를 사용하는 이유는 두가지
  1. 메소드가 호출될 때 마다 값이 복사되는 것을 방지하기 위함.
  2. 메소드에서 리시버 포인터가 가르키는 값을 수정하기 위함.

## 
