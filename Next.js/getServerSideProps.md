# getServerSideProps 사용해서 SSR 구현하기!

## 1. axios만 사용
- ```getServerSideProps```는 *```pages``` 폴더 안의 파일에서만 실행된다.*
- 컴포넌트에서 필요한 값들은 ```props```로 내려주기

```javascript
// pages/todoList.tsx

import React from 'react'
import ListContainer from '../components/ListContainer';
import apis from '../api/main';
import { GetServerSideProps } from 'next';
import { Props } from '../types';


const TodoList = ({todoData} : Props) => {  // pageProps로 전달받은 값 타입 설정

  console.log(todoData)
  return (
    <div className="container">
      <div className="flex flex-col mt-8">
        <h1>TO DO LIST</h1>
        <h2>with SSR  & React Query !</h2>
      </div>
      <form>
        <input 
          type="text" 
          className="main-input"
          placeholder="Write your plan"/>
        <button type="submit" className="btn1"><h2>Submit</h2></button>
      </form>
      <h2>Plans</h2>
      <ListContainer todoData={todoData}/>  // props로 non-page component에 값 전달
    </div>
  )
}

export const getServerSideProps : GetServerSideProps = async () => {

  const { data } = await apis.getTodos()  // 비동기 통신으로 data 받아오기

  return {
      props : {
          todoData : data  // props에 넣어준다.
      }
  }
}

export default TodoList;
```
- 받은 값을 다시 props로 넘겨주기
```javascript
// components/ListContainer.tsx

import React from 'react'
import { Props } from '../types';
import List from './List';

const ListContainer = ({todoData} : Props) => {  // 받아온 값 다시 타입 설정

  return (
    <div className="flex flex-col">
        { todoData.map((value, index) => (
            <List
                key={index}
                content={value.content}
                completed={value.completed}/>  // props로 다시 넘겨주기
        ))}
        
    </div>
  )
}

export default ListContainer;
```
- 값 사용해서 표시해주기
```javascript
// components/List.tsx

import React from 'react'
import { TodoType } from '../types';

const List = ({content, completed} : TodoType) => {
  return (
    <div className="card">
        <input type="checkbox" className="checkbox"/>
        <h2>{content}</h2>
        <button className="btn1"><h2>Delete</h2></button>
    </div>
  )
}

export default List;
```

<br>
<br>

## 2. react query 사용하기
- custom App 설정해주기
```javascript
// pages/_app.tsx

import React from "react";
import type { AppProps } from "next/app";
import "../styles/globals.css";
import "../styles/elements.css";
import { Hydrate, QueryClient, QueryClientProvider } from "react-query";
import { ReactQueryDevtools } from "react-query/devtools"

const App = ({ Component, pageProps }: AppProps) => {

 const [queryClient] = React.useState(() => new QueryClient())
 

  return (
    <QueryClientProvider client={queryClient}>
      <Hydrate state={pageProps.dehydratedState}>
        <Component {...pageProps} />
      </Hydrate>
      <ReactQueryDevtools/>
    </QueryClientProvider>
  )
};

// Hydrate를 이용해서 쿼리 캐싱과 수화 설정을 해준다.
// 이렇게 해야 구성 요소 수명 주기 당 QueryClient를 한 번만 생성한다.
// 데이터가 서로 다른 사용자와 요청간 공유되지 않는다.

export default App;
```
- ```getServerSideProps``` 사용해주기 (```pages```폴더 안 파일에서 사용)
```javascript
// pages/todoList.tsx

...

export const getServerSideProps : GetServerSideProps = async () => {

  const queryClient = new QueryClient();

  await queryClient.prefetchQuery(queryKeys.todos, getTodoData)  // prefetchQuery를 사용해준다.

  return {
      props : {
          dehydratedState: dehydrate(queryClient)  
      }
  }
}
```
- 값 불러오기
```javascript
const ListContainer = () => {

    const { data } = UseGetTodos();

  return (
    <div className="flex flex-col">
        { data.map((value : TodoType, index : number) => (
            <List
                key={index}
                content={value.content}
                completed={value.completed}/>
        ))}
        
    </div>
  )
}

export default ListContainer;
```

## 참고
- https://stackoverflow.com/questions/64136025/nextjs-getserversideprops-not-working-into-components
- https://react-query.tanstack.com/guides/ssr







