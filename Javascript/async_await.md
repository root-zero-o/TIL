# async, await
## 1. async, await 는 왜 사용하나요?
- ```fetch```,```then```을 통해 비동기 코딩을 할 경우, 동일한 이름의 메서드인 ```then()```을 연쇄적으로 호출하고 있어서, 어디서 문제가 발생한건지 찾기 어려움
- ```catch()```메서드를 사용한 예외 처리 : 동기 코드와 비동기 코드가 섞여있을 경우 난해해짐
- 여러 개의 Promise를 병렬 또는 중첩 : 코드 가독성이 떨어짐

## 2. async, await 써보자!
```javascript
// fetch 사용했을 경우
function fetchAuthorName(postId) {
  return fetch(`https://jsonplaceholder.typicode.com/posts/${postId}`)
    .then((response) => response.json())
    .then((post) => post.userId)
    .then((userId) => {
      return fetch(`https://jsonplaceholder.typicode.com/users/${userId}`)
        .then((response) => response.json())
        .then((user) => user.name);
    });
}

fetchAuthorName(1).then((name) => console.log("name:", name));
```
```javascript
// async, await 사용했을 경우
async function fetchAuthorName(postId) {
  const postResponse = await fetch(
    `https://jsonplaceholder.typicode.com/posts/${postId}`
  );
  const post = await postResponse.json();
  const userId = post.userId;
  const userResponse = await fetch(
    `https://jsonplaceholder.typicode.com/users/${userId}`
  );
  const user = await userResponse.json();
  return user.name;
}

fetchAuthorName(1).then((name) => console.log("name:", name));
```
- ```async```이 function 앞에 붙고, Promise를 리턴하는 모든 비동기 함수 호출부 앞에 ```await``` 추가
- ```await```키워드
    - ```async```키워드가 붙어있는 함수 내부에서만 사용 가능
    - 비동기 함수가 리턴하는 Promise로 부터 결과값 추출
    - ```await```키워드 사용하면 결과값을 얻을 수 있을 때까지 기다려줌. 따라서 동기 코드 처리와 동일한 흐름으로 코드 작성 가능
- 예외 처리
동기/비동기 구분 없이 ```try/catch```로 일관되게 예외 처리 가능
```javascript
async function fetchAuthorName(postId) {
  const postResponse = await fetch(
    `https://jsonplaceholder.typicode.com/posts/${postId}`
  );
  const post = await postResponse.json();
  const userId = post.userId;

  try {
    const userResponse = await fetch(
      `https://jsonplaceholder.typicode.com/users/${userId}`
    );
    const user = await userResponse.json();
    return user.name;
  } catch (err) {
    console.log("Faile to fetch user:", err);
    return "Unknown";
  }
}

fetchAuthorName(1).then((name) => console.log("name:", name));
```

## 참고
- https://www.daleseo.com/js-async-async-await/
