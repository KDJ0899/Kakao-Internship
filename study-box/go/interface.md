## 인터페이스 (Interface)

- 인터페이스는 메소드의 집합으로 정의.
- 메소드들의 구현되어 있는 타입의 값은 모두 인터페이스 타입의 값이 될 수 있습니다.

```go
type Square struct {
   Width  float32
   Height float32
}

type Triangle struct {
   Width  float32
   Height float32
}

func (s Square) Area() float32 {
   return s.Width * s.Height
}

func (t Triangle) Area() float32 {
   return t.Width * t.Height / 2
}

type Figure interface {
   Area() float32
}

func main() {
   var s, t Figure
   s = Square{2, 5}
   t = Triangle{2, 5}
   fmt.Println(s.Area())
   fmt.Println(t.Area())
}
```

- 타입이 인터페이스의 메소드들을 구현하면 인터페이스를 구현한게 됨. 이를 위해 명시적으로 선언할 게 없음.
- 암시적 인터페이스는 인터페이스를 정희한 패키지로부터 구현 패키지를 분리해줌.
- interface는 암시적으로 충족된다. 즉, 우리가 명시적으로 Squre는 Figure에 관련이다라고 해주지 않아도 알아서 찾는다는 뜻.

### 덕 타이핑(Duck Typing)

- 각 값이나 인스턴스의 실제 타입은 상관하지 않고 **구현된 메소드로만 타입을 판단**하는 방식.

- "만약 어떤 새가 오리처럼 걷고, 헤엄치고, 꽥꽥거리는 소리를 낸다면 나는 그 새를 오리라 부르겠다."

  ```go
  package main
  
  import "fmt"
  
  type Duck struct { // 오리(Duck) 구조체 정의
  }
  
  func (d Duck) quack() {     // 오리의 quack 메서드 정의
  	fmt.Println("꽥~!") // 오리 울음 소리
  }
  
  func (d Duck) feathers() { // 오리의 feathers 메서드 정의
  	fmt.Println("오리는 흰색과 회색 털을 가지고 있습니다.")
  }
  
  type Person struct { // 사람(Person) 구조체 정의
  }
  
  func (p Person) quack() {                           // 사람의 quack 메서드 정의
  	fmt.Println("사람은 오리를 흉내냅니다. 꽥~!") // 사람이 오리 소리를 흉내냄
  }
  
  func (p Person) feathers() { // 사람의 feathers 메서드 정의
  	fmt.Println("사람은 땅에서 깃털을 주워서 보여줍니다.")
  }
  
  type Quacker interface { // quack, feathers 메서드를 가지는 Quacker 인터페이스 정의
  	quack()
  	feathers()
  }
  
  func inTheForest(q Quacker) {
  	q.quack()    // Quacker 인터페이스로 quack 메서드 호출
  	q.feathers() // Quacker 인터페이스로 feathers 메서드 호출
  }
  
  func main() {
  	var donald Duck // 오리 인스턴스 생성
  	var john Person // 사람 인스턴스 생성
  
  	inTheForest(donald) // 인터페이스를 통하여 오리의 quack, feather 메서드 호출
  	inTheForest(john)   // 인터페이스를 통하여 사람의 quack, feather 메서드 호출
  }
  ```



- 타입이 특정 인터페이스를 구현하는지 검사하려면 다음과 같이 사용.

  interface{}(인스턴스).(인스턴스)

  ```go
  var donald Duck
  
  if v, ok := interface{}(donald).(Quacker); ok {
  	fmt.Println(v, ok)
  }
  ```



### 빈 인터페이스 사용하기

- 인터페이스에 아무 메소드도 정의되어 있지 않으면 모든 타입을 저장할 수 있다.

  ```go
  func f1(arg interface{}) { // 모든 타입을 저장할 수 있음
  }
  ```

  
