## **맵** **(Maps)**

- 맵은 값에 키를 지정합니다.
- 맵은 반드시 사용하기 전에 make를 명시 해야함 (주의, new가 아님)
- Map[Key타입]Value타입과 같이 선언
- Ex) var idMap map[int]string
- make를 수행하지 않은 nil에는 값을 할당할 수 없습니다.
- 맵 리터럴은 구조체 리터럴과 비슷하지만 key를 반드시 지정해야함.

```go
 var m = map[string]Vertex{

  "Bell Labs": Vertex{
	  40.68433, -74.39967,
  },
  "Google": Vertex{
	 37.42202, -122.08408,
  },
}
```

- 만약 가장 상위의 타입이 타입명이라면 리터럴에서 타입명을 생략해도 됨.

  ```
  “Bell Labs”: {40, -74} == “Bell Labs” : Vertex{40, -74}
  ```

- 맵의 요소를 삽입하거나 수정하기 : m[key] = value

- 요소 값 가져오기 : value = m[key]

- 요소 지우기 : delete(m, key)

- 키의 존재 여부 확인하기: value, ok = m[key]

Ok 값은 m에 key가 존재한다면 true 존재하지 않으면 false, elem은 타입에 따라 0(zero value)가 됨.
