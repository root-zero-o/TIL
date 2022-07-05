# createSelector
- store에서 데이터를 추출할 수 있도록 도와주는 유틸리티
- ```useSelector```의 결점을 보완해준다.
     - ```useSelector```가 실행될 때마다 이전에 참조하고 있던 객체 주소와 현재 주소의 차이가 발생함
     - 따라서 re-rendering 발생
 
```javascript
import { TodoState } from "./../type";
import { AnyAction, createSelector, ThunkDispatch } from "@reduxjs/toolkit";
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

 const todoSelector = (state : RootState) => state.todos;
  
  // selector 값을 메모이제이션한다.
  const selector = createSelector(
    todoSelector,
    (state) => state  // 여기서 데이터를 가공할 수 있다.
  )

  // useSelector를 사용해 데이터를 꺼내준다.
  const { lists, loading, error } = useSelector(selector);
  
  // 꺼내준 데이터를 리턴한다.
  return { lists, loading, error };
}
```
