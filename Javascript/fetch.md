# fetch()
## 1. 기본 구조
```javascript
fetch(url, options)
  .then((response) => console.log("response:", response))
  .catch((error) => console.log("error:", error));
```
- 첫 번째 인자로 URL, 두 번째 인자로 옵션 객체를 받고, Promise 타입의 객체 반환
- API 호출 성공시 응답(response) 객체를 resolve, 실패했을 경우에는 예외(error) 객체를 reject
- option 객체 : HTTP방식(method), HTTP 요청 헤더(headers), HTTP 요청 전문(body)등 설정 가능
- response 객체로부터는 HTTP 응답 상태(status), HTTP 응답 헤더(headers), HTTP 응답 전문(body) 등을 읽어올 수 있음

## 2. GET 호출
- ```fetch```함수는 디폴트로 GET 방식으로 작동(option 인자가 필요X)
```javascript
fetch("https://jsonplaceholder.typicode.com/posts/1").then((response) =>
  console.log(response)
);
```
```javascript
// 응답 객체
Response {status: 200, ok: true, redirected: false, type: "cors", url: "https://jsonplaceholder.typicode.com/posts/1", …}
```
- 대부분의 REST API들은 JSON 형태의 데이터를 응답하기 때문에, response 객체는 ```json()```메서드 제공
```javascript
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then((response) => response.json())
  .then((data) => console.log(data));
```
- ```json()```메서드를 호출하면 response 객체로부터 JSON 포맷의 응답 전문을 자바스크립트 객체로 변환하여 얻을 수 있음
```javascript
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit↵suscipit recusandae consequuntur …strum rerum est autem sunt rem eveniet architecto"
}
```

## 3. POST 호출
- 원격 API에서 관리하고 있는 데이터를 생성해야 할 때 필요
- method 옵션을 ```POST```로 지정해주고, ```headers``` 옵션을 통해 JSON포맷을 사용한다고 알려주어야 함
- 요청 전문을 JSON 포맷으로 직렬화하여 ```body``` 옵션에 설정해줌
```javascript
fetch("https://jsonplaceholder.typicode.com/posts", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    title: "Test",
    body: "I am testing!",
    userId: 1,
  }),
}).then((response) => console.log(response));
```
```javascript
// response 객체
Response {type: "cors", url: "https://jsonplaceholder.typicode.com/posts", redirected: false, status: 201, ok: true, …}
```

## 4. PUT, DELETE 호출
- 원격 API에서 관리하는 데이터의 수정과 삭제
### 1) PUT
-```method``` 옵션만 ```PUT```으로 설정한다는 점 이외에는 POST 방식과 매우 흡사
```javascript
fetch("https://jsonplaceholder.typicode.com/posts/1", {
  method: "PUT",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    title: "Test",
    body: "I am testing!",
    userId: 1,
  }),
})
  .then((response) => response.json())
  .then((data) => console.log(data));
```
```javascript
{title: "Test", body: "I am testing!", userId: 1, id: 1}
```

### 2) DELETE
- 보낼 데이터가 없어서 ```headers```와 ```body``` 옵션이 필요 없음
```javascript
fetch("https://jsonplaceholder.typicode.com/posts/1", {
  method: "DELETE",
})
  .then((response) => response.json())
  .then((data) => console.log(data));
```
```javascript
{}
```

## 참고
- https://www.daleseo.com/js-window-fetch/
- https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API
