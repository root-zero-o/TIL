# useState
## 1. 개념
- ```useState```: 컴포넌트에서 상태를 관리할 수 있게 해주는 Hook

## 2. 사용방법
- 리액트 패키지에서 ```useState``` 함수 불러오기
```javascript
import React, { useState } from 'react';
```
- useState의 기본 구문
```javascript
const [count, setCount] = useState(0);

// count라고 부르는 state 변수를 선언하고 0으로 초기화 한다
// 리액트는 해당 변수를 리렌더링할 때 기억하고, 가장 최근에 갱신된 값 제공
// count 변수의 값을 갱신하려면 setCount 호출
```

## 참고
- https://ko.reactjs.org/docs/hooks-state.html
- [벨로퍼트 모던 리액트](https://react.vlpt.us/basic/07-useState.html)
