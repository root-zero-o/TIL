# React Redux - 기본적인 흐름
## 1. 폴더 구조 잡기
```javascript
[public]
- index.html

 > [components] // 일반 컴포넌트들 보관
  - Counter.js
  
 > [containers] // redux store state 조회 & action을 dispatch 할 수 있는 Component
  - CounterContainer.js
  
 > [pages] // Routing 해 줄 페이지들
 
 > [redux]
  - configStore.js // store 생성
  >> [modules]
   - counter.js 
   - index.js  // 여러 개의 reducer를 하나로 합쳐주는 combineReducer가 있음
   - todo.js
```

## 2. 설치
```javascript
npm install react-redux redux
```

## 3. 전체적인 흐름
```
* 최상위 파일부터 단계적으로 Redux와 대화하듯이 만들어보기!
1. [src/index.js] 어디서부터 어디까지 Redux를 쓸거야? 
👉 Provider로 알려줄게
2. [src/redux/configStore.js] Redux를 쓰려면 store를 만들어야지! 
👉 store 만들었어. 안에 rootReducer 넣어줘!
3. [src/redux/modules/index.js] rootReducer에는 뭐가 들어가는데? 
👉 counter, todo 라는 2개의 리듀서로 구성되어 있어.
4. [src/redux/modules/counter.js] counter라는 리듀서는 뭐야? 안에 state랑 action이 어떻게 되어있어? 
👉 이렇게 되어있어!
   > 4-1. action은 어떻게 되어있는데? 
   👉 액션 타입 만들기
   > 4-2. action은 어떻게 만드는데? 
   👉 액션 생성함수 만들기
   > 4-3. state는 어떻게 되어있어? 
   👉 초기 상태 선언(initialState)
   > 4-4. 그럼 그 action이랑 state를 가지고 뭐할거야? 
   👉 리듀서 선언! 이렇게 action type에 따라 return할거야. 기억해놔!
5. [src/containers/CounterContainer] 좋아, 기억했어. 그럼 이 counter라는 리듀서를 구체적으로 어떻게 쓸거야? 
👉 useSelector을 사용해서 state를 가져오고, useDispatch를 이용해서 action을 실행할거야.
👉 이제 진짜 컴포넌트에서 실행할거니까, 내가 설명했던 것들을 props로 넘겨주자.
6. [src/components/Counter.js] 진짜 써보자! Counter라는 컴포넌트에서 지금까지 기억했던 것들로 실행하는거야!
```

## 4. 구체적인 코드
### 1. src/index.js
```javascript
import React from 'react';
import  ReactDOM  from 'react-dom/client';
import App from './App'
// Provider를 사용하기 위한 import
import { Provider } from 'react-redux';
// store를 곧 생성할 예정
import store from './redux/configStore'

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
    // 내가 사용하고싶은 전역상태관리의 범위만큼 Provider로 감싸고
    // 전역상태의 데이터가 들어있는 store를 넘겨준다
    <Provider store={store}>
        <App/>
    </Provider>
);
```

## 2. src/redux/configStore.js
```javascript
import { createStore } from "redux";
// 모듈 안에서 rootReducer 가져와서 Store 생성 예정
import rootReducer from './modules';

// 생성
const store = createStore(rootReducer);
export default store;
```

## 3. src/redux/modules/index.js
```javascript
import { combineReducers } from "redux";
import counter from './counter';
import todo from './todo';

// counter, todo reducer 들을 이렇게 합침
const rootReducer = combineReducers({
  counter,
  todo, // 이런식으로 reducer을 합침
});

export default rootReducer;
```

## 4. src/redux/modules/counter.js
```javascript
/* 1단계 : 액션 타입 만들기 */
// 다른 모듈과 이름 중복방지를 위해 이렇게 만듦
const SET_DIFF = 'counter/SET_DIFF'; // 이게 뭐지? 폴더이름? 파일이름?
const INCREASE = 'counter/INCREASE';
const DECREASE = 'counter/DECREASE';

/* 2단계 : 액션 생성함수 만들기 */
// 내가 밖에서 사용할 액션 함수를 만든다. export 빼먹지 말기
export const setDiff = diff => ({ type: SET_DIFF, diff}); // 여기서 diff는 key값
export const increase = () => ({ type: INCREASE }); 
export const decrease = () => ({ type: DECREASE });

/* 3단계 : 초기 상태 선언 */
// 제일 처음 store가 가질 초기값!
const initialState = {
    number: 0, // 화면에 보여줄 초기값
    diff: 1 // input에 띄워줄 초기값 
}

/* 4단계 : 리듀서 선언 */
// 리듀서는 합치는 애가 받아야 함 -> export
export default function counter( state = initialState, action ) {

    // 사용할 액션타입에 따른 함수만 적용되게끔 switch case 사용!
    switch (action.type){

        // SET_DIFF 타입이라면, 아래 case 발동
        case SET_DIFF:
            return {...state, diff: action.diff}; 
        
        // INCREASE 타입이면, 아래 case 발동
        case INCREASE:
            return {...state, number: state.number + state.diff};

        // DECREASE 타입이면, 아래 case 발동
        case DECREASE:
            return {...state, number: state.number - state.diff};

        default:
            return state;
    }
}
```

## 5. src/containers/CounterContainer
```javascript
import React from 'react';

// 값을 수정하기 위해 import
import { useSelector, useDispatch } from 'react-redux';
import Counter from '../components/Counter'; 

// counter reducer에서 가져온 액션 함수
import { increase, decrease, setDiff } from '../redux/modules/counter';

function CounterContainer() {

    // useSelector는 리덕스 스토어의 상태를 조회하는 Hook
    // 비구조화로 객체의 경우 좌항과 우항이 매칭된다.
    const { number, diff } = useSelector(state => ({
        number : state.counter.number, //
        diff : state.counter.diff //  
    }));

    // 그냥 CRUD 할때 무조건 dispatch를 써야해. 그래서 선언
    const dispatch = useDispatch(); //

    // 함수를 만드는데, 그 함수를 dispatch를 이용해서 reducer에서 만든 애들을 불러와야해
    const onIncrease = () => dispatch(increase());
    const onDecrease = () => dispatch(decrease());
    const onSetDiff = diff => dispatch(setDiff(diff));

    return (
        <Counter
            //상태와
            number={number}
            diff={diff}
            // 액션을 디스패치하는 함수들을 props로 넣어줌
            onIncrease={onIncrease}
            onDecrease={onDecrease}
            onSetDiff={onSetDiff}
        />
    );
}

export default CounterContainer;
```

## 6. src/components/Counter.js
```javascript
import React from "react";

// Container에서 props로 받은 것들을 파라미터에 작성
function Counter({ number, diff, onIncrease, onDecrease, onSetDiff }) {

    // 버튼 이벤트
    const onChange = e => {
        onSetDiff(parseInt(e.target.value, 10)); // e.target.value를 10진법으로 변환해서 넣어. 넣으면 diff
    };

    return (
        <div>
            {/* 보여줄 숫자 */}
            <h1>{number}</h1>
            <div>
                {/* input창에 띄워줄 숫자, diff의 값을 가져와서 보여줌 */}
                <input type="number" value={diff} min="1" onChange={onChange}/>
                <button onClick={onIncrease}>+</button>
                <button onClick={onDecrease}>-</button>
            </div>
        </div>
    );
}

export default Counter;
```

## 참고 및 출처
- https://devkevin0408.tistory.com/202
- https://github.com/kordobby/amazon/blob/main/React/Redux/2.redux_guide.md
