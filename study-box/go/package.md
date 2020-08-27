## 패키지

- Go는 패키지를 통해 **코드의 모듈화, 코드의 재사용 기능**을 제공.
- 패키지를 사용해서 작은 단위의 컴포넌트를 작성하고, 이러한 작은 패키지들을 활용해서 프로그램을 작성할 것을 권장.
- 패키지 내에는 함수, 구조체, 인터페이스, 메서드 등이 존재하는데, 이들의 이름 첫문자가 **대문자로 시작하면 Public 소문자는 non-public**



### Main Package

- 일반적으로 패키지는 라이브러리로서 사용되지만, "main"패키지는 Go Compiler에 의해 특별하게 인식됨.
- main패키지는 컴파일러가 공유 라이브러리가 아닌 실행프로그램으로 만듬.
- 패키지를 공유 라이브러리로 만들 때에는, main패키지나 main함수를 사용해서는 안된다.



### init 함수와 alias

- init함수는 패키지가 로드되면서 실행되는 함수로, **별도의 호출 없이 자동으로 호출됨.**

  ```go
  var pop map[string]string
   
  func init() {   // 패키지 로드시 map 초기화
      pop = make(map[string]string)
  }
  ```

- 경우에 따라 패키지를 import 하면서 단지 그 패키지 안의 init() 함수만을 호출하고자 하는 케이스가 있다. 이런 경우는 패키지 import 시 _ 라는 alias 를 지정한다. 아래는 other/xlib 패키지를 호출하면서 _ alias를 지정한 예이다.

  ```go
  package main
  import _ "other/xlib"
  ```

- 만약 패키지 이름이 동일하지만, 서로 다른 버젼 혹은 서로 다른 위치에서 로딩하고자 할 때는, 패키지 alias를 사용해서 구분할 수 있다.

  ```go
  import (
      mongo "other/mongo/db"
      mysql "other/mysql/db"
  )
  func main() {
      mondb := mongo.Get()
      mydb := mysql.Get()
  }
  ```

