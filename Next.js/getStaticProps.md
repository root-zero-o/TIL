# getStaticProps로 SSG 구현하기

## 1. axios만 사용
- ```getStaticProps()``` 안에서 서버와 비동기 통신하기
```typescript
// pages/index.tsx

export async function getStaticProps() {
  try {
    const { data } = await apis.getTodos();
    return {
      props: {
        todoData : data  // props안에 todoData라는 key를 만들고, value로 서버에서 가져온 data를 넣는다.
      }
    }
  }
  catch(err){
    console.log(err)
  }
}
```
- 넣어준 props를 받는 곳
```typescript
// pages/_app.tsx

import React from "react";
import type { AppProps } from "next/app";
import "../styles/globals.css";
import "../styles/elements.css";
import { QueryClientProvider } from "react-query";
import { ReactQueryDevtools } from "react-query/devtools"

const App = ({ Component, pageProps }: AppProps) => {

 const [queryClient] = React.useState(() => new QueryClient())
 

  return (
    <QueryClientProvider client={queryClient}>
        <Component {...pageProps} />  // Component 자리에는 페이지가 들어간다.
                                      // pageProps에 props로 넣어줬던 데이터가 들어간다.
      <ReactQueryDevtools/>
    </QueryClientProvider>
  )
};

export default App;
```
- 타입 맞춰주기
```typescript
// pages/ index.tsx

type Props = {
  todoData : TodoType[];  // 기존 데이터 타입으로 설정했던 TodoType의 배열이라고 타입을 설정해준다.
}

const Index = ({todoData} : Props) => {  // 여기에서 타입을 설정해준다.
...  // 이제 Props로 받아온 데이터를 사용해준다.

}

```
<br>
<br>

## 2. React Query 함께 사용
*혼자 구글링+스택오버플로우로 공부해서 구현했으나.. 오류가 있을 수 있습니다. 지적은 언제든 환영입니다🤩*
- hydrate 설정
```typescript
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

// Hydrate를 이용해서 쿼리 캐싱과 hydrate 설정을 해준다.
// 이렇게 해야 구성 요소 수명 주기 당 QueryClient를 한 번만 생성한다.
// 데이터가 서로 다른 사용자와 요청간 공유되지 않는다.

export default App;
```
- ```getStaticProps()```안에서 서버와 비동기통신
```typescript
// pages/index.tsx

export async function getStaticProps() {
  const queryClient = new QueryClient()

  const getTodoData = async () => {
    const { data } = await apis.getTodos()
    return data  // axios를 사용할 때는 .data를 꺼내서 그걸 넘겨줘야 오류가 안남!
  }

  try {
    await queryClient.prefetchQuery(queryKeys.todos, getTodoData)  // prefetchQuery 이용하기
                                                                   // 첫 번째는 쿼리키, 두 번째는 서버랑 통신하는 함수
    return {
      props: {
        dehydratedState : dehydrate(queryClient)  // 이런 형태로 props를 넘겨준다.
      }
    }
  }
  catch(err){
    console.log(err)
  }
}
```
- 커스텀 훅으로 값 불러와주기
```typescript
// pages/index.tsx

const Index = () => {

  const router = useRouter();

  const { data } = UseGetTodos();  // 커스텀 훅(useQuery)으로 값을 불러와주어야 함
                                   // 커스텀 훅 사용하지 않을 경우 useQuery 등 사용

  return (
    <div className='flex flex-col items-center justify-center space-y-5'>
      <span className="font-serif text-5xl">TO DO LIST</span>
      <span className="font-serif text-lg ">You have {data?.length} works to do !</span>
      <button 
        className='btn1'
        onClick={() => router.push("/todoList")}>
          <h2>GO</h2>
      </button>
    </div>
  )
}
```

## 참고
- https://velog.io/@hhhminme/Next.js%EC%97%90%EC%84%9C-Axios%EB%A5%BC-%ED%86%B5%ED%95%B4-getStaticProps%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EC%9E%90feat.-typescirpt
- https://stackoverflow.com/questions/71630615/next-js-error-serializing-dehydratedstate-queries0-state-data-config-adapter
- https://react-query.tanstack.com/guides/ssr
- https://gingerkang.tistory.com/123
- https://velog.io/@familyman80/Culture-Place%EC%A0%9C%EC%9E%91%EA%B8%B0-3-Nextjs%EC%99%80-%ED%95%A8%EA%BB%98%ED%95%98%EB%8A%94-React-Query-1-
