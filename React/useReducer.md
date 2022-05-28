# useReducer
## 1. ```reducer``` 란?
- 현재 상태와 액션 객체를 파라미터로 받아와서 새로운 상태를 반환해주는 함수
```javascript
function reducer(state, action) {
  // 새로운 상태를 만드는 로직
  // const nextState = ...
  return nextState;
}
```
- ```reducer```에서 반환하는 state는 곧 컴포넌트가 지닐 새로운 state가 됨
- ```action```은 업데이트를 위한 정보를 가짐. 주로 ```type``` 값을 지닌 객체 형태로 사용하나, 꼭 따라야 할 규칙은 따로 없음
- ```action``` 예시
```javascript
// 카운터에 1을 더하는 액션
{
  type: 'INCREMENT'
}
// 카운터에 1을 빼는 액션
{
  type: 'DECREMENT'
}
// input 값을 바꾸는 액션
{
  type: 'CHANGE_INPUT',
  key: 'email',
  value: 'tester@react.com'
}
// 새 할 일을 등록하는 액션
{
  type: 'ADD_TODO',
  todo: {
    id: 1,
    text: 'useReducer 배우기',
    done: false,
  }
}
```
## 2. ```useReducer```
```javascript
const [state, dispatch] = useReducer(reducer, initialState);
```
- ```state``` : 우리가 앞으로 컴포넌트에서 사용할 수 있는 상태
- ```dispatch``` : 액션을 발생시키는 함수( ```dispatch({ type: 'INCREMENT'})``` 와 같이 사용)
- ```useReducer``` 첫 번째 파라미터 : ```reducer``` 함수
- ```useReducer``` 두 번째 파라미터 : 초기 상태

## 3. 사용 예시
```javascript
import React, {useReducer} from 'react'

function reducer(state, action) {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1;
    case 'DECREMENT':
      return state -1;
    default:
      return state; 
  }
}

function Counter() {
    const [number, dispatch] = useReducer(reducer, 0)

    const onIncrease = () => {
        dispatch({ type: 'INCREMENT'});
    };

    const onDecrease = () =>{
        dispatch({ type: 'DECREMENT'});
    }

  return (
    <div>
        <h1>{number}</h1>
        <button onClick={onIncrease}> +1</button>
        <button onClick={onDecrease}> -1</button>
    </div>
  );
}

export default Counter;
```
## 4. ```useReducer```, ```useState``` 뭘 써야하나요?
- 컴포넌트에서 관리하는 값이 하나이고, 그 값이 단순한 숫자, 문자열 또는 boolean값이면 ```useState```가 편함
- 컴포넌트에서 관리하는 값이 여러개라서 state의 구조가 복잡해지면 ```useReducer```로 관리하는 것이 편함
- 상황에 따라 고민해서 사용하자 !

## 참고
- [벨로퍼트 모던 리액트](https://react.vlpt.us/basic/20-useReducer.html)
- https://www.daleseo.com/react-hooks-use-reducer/

