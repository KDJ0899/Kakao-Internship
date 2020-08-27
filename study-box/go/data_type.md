## **자료형**

### **기본 자료형**

```go
bool

string

int int8 int16 int32 int64

uint uint8 uint16 uint32 uint64 uintptr

byte // uint8의 다른 이름(alias) 

rune // int32의 다른 이름(alias)

   	// 유니코드 코드 포인트 값을 표현합니다. 

float32 float64 

complex64 complex128 복소수
```

### 문자열

- 문자열은 ' ' 혹은 " "사용하여 표현가능.

- ' '로 둘러 싸인 문자열은 별도로 해석하지 않고 Raw String 그대로의 값을 갖는다. 예를 들어 \n을 NewLine으로 해석하지 않음.

  **복수 라인의 문자열을 표현**할 때 자주 사용.

- " "로 둘러 싸인 문자열은 복수 라인에 걸쳐 쓸 수 없으며, 인용부호 안의 문자열들은 특별한 의미로 해석.

  

### 형 변환 (Type Conversion)

- Go에서 형 변환은 명시적으로 지정해 주어야 함. 명시적 지정이 없이 변환이 일어나면 런타임 에러 발생.

  ```go
  var i int = 100
  var u uint = uint(i)
  var f float32 = float32(i) 
  
  str := "ABC"
  bytes := []byte(str)
  str2 := string(bytes)
  ```

  
