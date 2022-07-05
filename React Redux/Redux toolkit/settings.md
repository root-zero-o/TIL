# Redux toolkit settings

- 설치하기
```
yarn add @reduxjs/toolkit
yarn add react-redux
yarn add next-redux-wrapper
```

- 폴더구조
```
├── store
│   ├── modules
│   │   ├── todosSlice.ts (리듀서 모듈)
│   │   └── index.ts (리듀서 모듈 통합해서 루트 리듀서 생성)
│   └── configStore.ts (store 생성, 미들웨어 설정)
└── styles
```

- store/modules/index.ts
```javascript
import { combineReducers } from 'redux';
import todos from './todosSlice';

// 루트 리듀서
const rootReducer = combineReducers({ todos }); // 리듀서가 추가되면 여기에 넣는다.

export default rootReducer;

// 루트 리듀서의 반환값를 유추해준다.
// 추후 이 타입을 컨테이너 컴포넌트에서 불러와서 사용해야 하므로 export
export type RootState = ReturnType<typeof rootReducer>;
```


- store/configStore.ts
```javascript
import { configureStore, getDefaultMiddleware } from '@reduxjs/toolkit';
import { createWrapper } from 'next-redux-wrapper';
import rootReducer from './modules';

// configureStore
// - 기본 미들웨어로 redux-thunk를 자동으로 추가해준다.
// - Redux DevTools Extension을 자동으로 활성화해준다.

export const makeStore = () => configureStore({ 
    reducer : rootReducer, 
    middleware: (getDefaultMiddleware) => getDefaultMiddleware()
    // devTools : boolean 값으로 개발자 도구 on/off
    // preloadedState: store 초기값 설정
})

export type AppStore = ReturnType<typeof makeStore>

const wrapper = createWrapper<AppStore>(makeStore)
  
export default wrapper;
```

- pages/_app.tsx
```javascript
import '../styles/globals.css'
import type { AppProps } from 'next/app';
import  wrapper  from "../store/configStore";

function MyApp({ Component, pageProps }: AppProps) {
  return <Component {...pageProps} />
}

// wrapper로 app을 감싸준다.
export default wrapper.withRedux(MyApp)
```
