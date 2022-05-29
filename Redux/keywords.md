# Redux에서 사용되는 키워드
## 1. 액션(Action)
- 상태에 어떠한 변화가 필요하게 될 때, 액션을 발생시킴
- 액션의 형식
```javascript
{
  type: "TOGGLE_VALUE",  // 액션 객체는 type 필드를 필수적으로 가지고 있어야 함
  data: {
    id: 0,
    text: "리덕스"
  } 
}
```
## 2. 액션 생성함수(Action Creator)
- 액션을 만드는 함수
- 파라미터를 받아와서 액션 객체 형태로 만들어줌
- 나중에 컴포넌트에서 더욱 쉽게 액션을 발생시키기 위해 사용(그래서 보통 함수 앞에 ```export``` 키워드를 붙여 다른 파일에서 불러와 사용
```javascript
export function addTodo(data) {
  return {
    type: "ADD_TODO",
    data
  };
}
```
## 3. 리듀서(Reducer)
- 변화를 일으키는 함수
- state와 action을 파라미터로 받아, 새로운 상태를 만들어 반환함
```javascript
function counter(state, action) {
  switch (action.type) {
    case 'INCREASE':
      return state + 1;
    case 'DECREASE':
      return state - 1;
    default:
      return state;
  }
}
```
- ```useReducer```와 달리 ```default``` 부분에 ```state```를 그대로 반환하도록 작성해야 함
- 여러 개의 리듀서를 만들고 이를 합쳐서 루트 리듀서(Root Reducer)를 만들 수 있음(작은 리듀서 = 서브 리듀서 라 부름)

## 4. 스토어(Store)
- 한 애플리케이션 당 하나의 스토어를 만듦
- 스토어 안에는 현재의 state와 리듀서, 몇 가지 내장 함수들이 있음

## 5. 디스패치(dispatch)
- 스토어의 내장함수 중 하나로, 액션을 발생 시키는 것(액션을 파라미터로 전달함)
- 디스패치를 호출하면, 스토어는 리듀서 함수를 실행시켜 새로운 state를 만들어줌

## 6. 구독(subscribe)
- 스토어의 내장함수 중 하나로, 함수 형태의 값을 파라미터로 받아옴
- subscribe 함수에 특정 함수를 전달해주면, 액션이 디스패치 되었을 때 마다 전달해 준 함수가 호출됨
- react-redux 라는 라이브러리에서 제공하는 ```connect``` 함수 또는 ```useSelector``` Hook 을 사용하여 리덕스 스토어의 상태에 구독함
