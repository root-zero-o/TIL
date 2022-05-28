# useCallback
## 1. 개념
- ```useCallback()```은 함수를 memoization하기 위해 사용되는 hook 함수!
- 기본 구문
     - 첫 번째 인자 : 넘어온 함수
     - 두 번째 인자 배열 : 배열 내의 값이 변경될 때까지 저장해놓고 재사용
```javascript
const memoizedCallback = useCallback(함수, 배열);
```
- ```useCallback```사용 전 : 컴포넌트가 렌더링될 때 마다 새로운 함수 생성
```javascript
const add = () => x + y;
```
- ```useCallback``` 사용 : 함수가 의존하는 값(x, y)이 바뀌지 않는 한 기존 함수를 계속 반환
```javascript
const add = useCallback(() => x + y, [x, y]);
```
*but 컴포넌트가 렌더링될 때마다 함수를 새로 선언하는 것은 성능상 큰문제가 없다. 그럼 언제 써?🤷*

- JavaScript에서는 함수도 객체로 취급이 되기 때문에 메모리 주소에 의한 reference비교가 일어남
- 이러한 특성은 React 컴포넌트 함수 내에서 어떤 함수를 다른 함수의 인자로 넘기거나 자식 컴포넌트의 prop으로 넘길 때 성능문제 야기
- 이러한 특성 때문에 사용한다!

## 2. 언제 사용해? : 의존 배열로 함수를 넘길 때
- 많은 React hook 함수들이 불필요한 작업을 줄이기 위해 두 번째 인자로 첫 번째 함수가 의존해야 하는 배열을 받음
- 이때 배열 안에 함수가 들어간다면?
```javascript
import React, { useState, useEffect } from "react";

function Profile({ userId }) {
  const [user, setUser] = useState(null);

  const fetchUser = () =>
    fetch(`https://your-api.com/users/${userId}`)
      .then((response) => response.json())
      .then(({ user }) => user);

  useEffect(() => {
    fetchUser().then((user) => setUser(user));
  }, [fetchUser]);

  // ...
}
```
- 위 코드의 문제점
    - 컴포넌트에서 API를 호출하는 코드는 ```fetchUser```함수가 변경될 때만 호출됨
    - 하지만 컴포넌트가 렌더링 될 때마다 ```fetchUser```는 함수이기 때문에 새로운 참조값으로 변경이 됨
    - 따라서 전과 다르다고 판단되어 ```useEffect()```함수가 호출되고, 또 ```user```값이 바뀌고, 또 렌더링이 되고, 또 ```useEffect```가 호출되고..
    - 👉 이럴 때 ```useCallback```을 사용한다!
```javascript
import React, { useState, useEffect } from "react";

function Profile({ userId }) {
  const [user, setUser] = useState(null);

  const fetchUser = useCallback(
    () =>
      fetch(`https://your-api.com/users/${userId}`)
        .then((response) => response.json())
        .then(({ user }) => user),
    [userId]
  );

  useEffect(() => {
    fetchUser().then((user) => setUser(user));
  }, [fetchUser]);

  // ...
}
```
- 이렇게 ```useCallback```을 사용하면 컴포넌트가 렌더링되어도 ```fetchUser```의 참조값을 동일하게 유지할 수 있음
- 따라서 의도했던 대로 ```userID```값이 변경되어야만 ```useEffect()```가 호출됨!

## 참고
- https://www.daleseo.com/react-hooks-use-callback/
- [벨로퍼트 모던 리액트](https://react.vlpt.us/basic/18-useCallback.html)
