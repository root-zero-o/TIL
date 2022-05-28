# React.memo
## 1. 개념
- UI 성능을 증가시키기 위해, React는 고차 컴포넌트(Higher Order Component, HOC)인 ```React.memo()```를 제공함
- 컴포넌트가 ```React.memo()```로 래핑되면, React는 컴포넌트를 렌더링하고 결과를 memoizing 👉 다음 렌더링 때 props가 같으면 memoizing된 내용 재사용
```javascript
React.memo(Component, [areEqual(prevProps, nextProps)]); 
// 비교 방식을 수정하고 싶으면 두 번째 매개변수로 비교함수를 만들어 넘겨주면 됨
```

## 2. 언제 쓰면 될까?
- 컴포넌트가 같은 props로 자주 렌더링될 때
- 무겁고 비용이 큰 연산이 있는 경우
- but 이러한 상황 이외에는 ```React.memo```를 사용할 필요가 없을 가능성이 높음!(성능적 이점이 없다면 사용하지 말 것🙅‍♂️)
- 동일한 props 값을 전달하더라도 새로운 콜백 때문에 리렌더링을 하게 되는 경우, 새로운 콜백이 발생하지 않게 ```useCallback()```을 사용

## 참고
- https://ui.toast.com/weekly-pick/ko_20190731
- https://velog.io/@qwe6293/React-React.memo-%EC%96%B8%EC%A0%9C-%EC%82%AC%EC%9A%A9%ED%95%98%EC%A7%80
- [벨로퍼트 모던 리액트](https://react.vlpt.us/basic/19-React.memo.html)
