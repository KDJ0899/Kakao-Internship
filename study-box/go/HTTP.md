## 웹서버 (HTTP)

### Http.Handler 인터페이스

```go
type Handler interface{
	ServeHTTP(w ResponseWriter, r *Request)
}
```



### Http.HandleFunc

- HandleFunc은 func(ResponseWriter, *Request)의 형태를 가진 함수를 핸들러 형태로 바꿔줌.
- 실제로 ServeHTTP 인터페이스를 구현하지 않고, Handler와 같은 파라미터를 가진 함수만 만들어 주면, 쉽게 핸들러를 사용할 수 있음.



### ServeMux

- ServeMux는 HTTP 요청 멀티플렉서
- 요청 URL에 따라 요청 URL에 대응하여 적절한 핸들러로 연결.
- DefaultServeMux는 ServaMux의 "인스턴스"
- ServeMux는 URL매칭을 처리할 수 있는 패턴 변수를 지원하지 않음.

