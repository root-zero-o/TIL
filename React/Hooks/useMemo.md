# useMemo
## 1. memoization이란?
- 기존에 수행한 연산의 결과값을 어딘가에 저장해두고, 동일한 입력이 들어오면 재활용하는 프로그래밍 기법을 말함
- memoization을 적절히 활용하면 중복 연산을 피할 수 있기 때문에 메모리를 조금 더 쓰더라도 애플리케이션의 성능을 최적화할 수 있음
- 렌더링이 발생했을 때, 이전 렌더링과 현재 렌더링 간의 값이 동일한 경우, 함수를 호출하는 대신 기존 메모리에 저장해두었던 값 사용
- memoization을 간편하게 사용할 수 있게 해주는 것이 바로 ```useMemo``` hook!

## 2. 사용방법
- ```useMemo```를 사용하지 않은 함수 : ```compute```함수의 연산이 복잡해 시간이 오래 걸리면, 렌더링이 필요할 때마다 UI 지연
```javascript
function MyComponent({ x, y }) {
  const z = compute(x, y);
  return <div>{z}</div>;
}
```
- 위 함수에 memoization 적용
```javascript
function MyComponent({ x, y }) {
  const z = useMemo(() => compute(x, y), [x, y]);
  return <div>{z}</div>;
}
```
- ```useMemo```의 2개의 인자
    - 첫 번째 : 결과값을 생성해주는 팩토리 함수
    - 두 번째 : 기존 결과값 재활용 여부의 기준이 되는 입력값 배열(위의 함수에서는 x, y값이 동일한 경우 저장한 값 재활용)
- import
```javascript
import React, { useMemo } from "react";
```

## 3. 주의할 점
- ```useMemo``` hook 함수를 남용하면, 컴포넌트의 복잡도가 올라가기 때문에 코드를 읽기 어려워지고 유지보수성이 떨어짐
- ```useMemo```가 적용된 레퍼런스는 재활용을 위해 garbage collection에서 제외되기 때문에 메모리를 더 씀
- 실제 웹 프로젝트에서 사용할 일은 많지 않다!

## 참고
- https://www.daleseo.com/react-hooks-use-memo/
- https://ko.reactjs.org/docs/hooks-reference.html
- [벨로퍼트 모던 리액트](https://react.vlpt.us/basic/17-useMemo.html)
