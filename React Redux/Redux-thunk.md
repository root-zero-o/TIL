# Redux-thunk 사용하기

## 1. 설치
```
yarn add redux-thunk
```

## 2. 적용하기
### src/redux/index.js
```javascript
import { createStore } from "redux";
import { applyMiddleware } from "redux";
import thunk from "redux-thunk"; // 1. 먼저 import 해주고

import rootReducer from './modules';

const middlewares = [thunk]; // 2. 미들웨어가 추가되면 여기에 추가
const enhancer = applyMiddleware(...middlewares);
const store = createStore(rootReducer, enhancer); // 3. store 안에 넣어준다
export default store; 
```

## 3. 사용하기
