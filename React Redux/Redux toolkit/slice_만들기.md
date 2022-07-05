# Slice 만들기 

### 1. createAsyncThunk

```javascript
// store/modules/todosSlice.ts

export const fetchTodos = createAsyncThunk("todo/fetchTodos", async() => {
    const { data } = await apis.getTodos() // axios instance 사용
    return data;
})
```
- createAction의 비동기 버전을 위해 제안되었다.
- 액션타입 문자열, 프로미스를 반환하는 콜백함수 두 가지를 인자로 받는다.
- 주어진 액션타입 문자열을 접두어로 사용하는 액션타입을 생성한다.

### 2. initialState
```javascript
const initialState : InitialState = { // 타입 설정은 필수 !
    lists : [],
    loading: false,
    error: false,
}
```

### 3. createSlice
```javascript
const todosSlice = createSlice({
    name: "todos",
    initialState,
    reducers: {},

    // extraReducers
    // - createSlice가 생성한 액션타입 외 다른 액션타입에 응답할 수 있도록 한다.
    // - 아래 함수에서 'todo/fetchTodo' 액션 타입과 상응하는 리듀서는 정의되어 있지 않다.
    //   하지만 슬라이스 외부에서 액션 타입을 참조하여 상태를 변화시킬 수 있다. 
    // - 프로미스 진행 상태에 따라 리듀서를 실행할 수 있다.
    
    extraReducers: builder => {
        builder
        .addCase(fetchTodos.pending, state => {
            state.loading = true;
        })
        .addCase(fetchTodos.fulfilled, (state, action) => {
            state.loading = false;
            state.lists = action.payload;
            state.error = false;
        })
        .addCase(fetchTodos.rejected, (state) =>{
            state.loading = false;
            state.lists = [];
            state.error = true;
        })
        // .addMatcher(matcher, reducer) : 새로 들어오는 모든 액션에 대해 주어진 패턴과 일치하는지 확인 후 reducer 실행
        // .addDefaultCase(reducer) : 그 어떤 케이스 리듀서나 matcher 리듀서도 실행되지 않았을 때, 기본 리듀서 실행
    }
})

export default todosSlice.reducer;
```
- createAction, createReducer 함수가 내부적으로 사용된다.
- name을 따라서 리듀서와 액션 생성자, 액션 타입을 자동으로 생성한다.

### 4. custom Hook 만들기
```javascript
import { TodoState } from "./../type";
import { AnyAction, ThunkDispatch } from "@reduxjs/toolkit";
import { useEffect } from "react";
import { useDispatch, useSelector } from "react-redux";
import { RootState } from "../store/modules";
import { fetchTodos } from "../store/modules/todosSlice";

// 타입을 설정해준다. 
type AppDispatch = ThunkDispatch<TodoState, any, AnyAction>;

// custom Hook
export default function useGetTodos() {

  const dispatch: AppDispatch = useDispatch();

  // 미들웨어를 실행해서 서버에서 데이터를 가져온다.
  // 리듀서를 통해 서버에서 가져온 데이터가 store에 들어간다.
  useEffect(() => {
    dispatch(fetchTodos());
  }, [dispatch]);

  // useSelector를 통해 store에서 데이터를 꺼내준다.
  const { lists, loading, error } = useSelector(
    (state: RootState) => state.todos
  );
  // 꺼내준 데이터를 리턴한다.
  return { lists, loading, error };
}
```

### 5. 데이터 사용하기
```javascript
// components/CardContainer.tsx

import React from 'react'
import { Card } from './Card'
import useGetTodos from "../Hooks/todosHook";
import Input from './Input';

export const CardContainer = () => {

    const {lists, loading, error} = useGetTodos(); // 한 줄로 간단하게 꺼내기 !

  return (
    <div className="flex flex-col item-center p-10">
        <Input/>
        <div className='m-auto grid gap-10 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4'>  
          { lists?.map((val, idx) => (
            <Card 
              key={idx}
              id={val.id}
              content={val.content}
              completed={val.completed}
              />
          ))}
        </div>
        
    </div>
  )
}

```

## 참고
- https://kimyang-sun.tistory.com/entry/%EB%A6%AC%EC%95%A1%ED%8A%B8-%EB%A6%AC%EB%8D%95%EC%8A%A4-%ED%88%B4%ED%82%B7%EC%9C%BC%EB%A1%9C-%EC%83%81%ED%83%9C%EA%B4%80%EB%A6%AC-React-Redux-Toolkit
- http://blog.hwahae.co.kr/all/tech/tech-tech/6946/
- https://redux-toolkit.js.org/usage/usage-with-typescript
