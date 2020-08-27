## **레인지** **(Range,** **범위)**

- For 반복문에서 range를 사용하면 슬라이스나 맵을 순회할 수 있음.

- For index, value := range(array) , 인덱스와 값 순서.

- _를 이용해서 인덱스나 값을 무시할 수 있습니다.

  ```go
  pow := make([]int, 10)
  
  for i := range pow {
    pow[i] = 1 << uint(i)
  }
  
  for _, value := range pow {
    fmt.Printf("%d\n", value)
  }
  ```

