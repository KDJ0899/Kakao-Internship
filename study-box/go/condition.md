## **조건문**

- If문은 C와 JAVA와 비슷함. ()소괄호가 필요 없음.

- 조건문 앞에 짧은 문장을 실행할 수 있음. 단, 짧은 실행문을 통해 선언된 변수는 if안쪽 범위에서만 사용가능.

- If에 짧은 명령문을 통해 선언한 변수는 else블럭 안에서도 사용가능.

  ```go
  if v := math.Pow(x, n); v < lim {
          return v
      } else {
          fmt.Printf("%g >= %g\n", v, lim)
      }
      // can't use v here, though
      return lim
  ```

  
