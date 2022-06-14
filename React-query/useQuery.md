# useQuery 사용해서 GET 하기

### 1. 컴포넌트에 사용
- import 해주기
```javascript
import { useQuery } from "react-query";
```
- fetcher 함수 만들기
```javascript
const fetcher = async () => {
        const { data } = await apis.getPosts();
        return data;
      };
      
const { data, error, isError, isLoading } = useQuery("유니크 키 값", fetcher);
```
👉 여기서 data를 꺼내서 그냥 사용하면 됨 ! *(이렇게 간단할수가)*

### 2. 커스텀 Hook 만들기
- src/Hooks/useGetPosts.jsx
```javascript
import React from 'react'
import { useQuery } from "react-query";
// import axios instance
import apis from '../api/main';

export const useGetPosts = () => {
    const fetcher = async () => {
        const { data } = await apis.getPosts();
        return data;
      };

  return useQuery("posts", fetcher); 
}
```
- src/components/CardContainer.jsx
```javascript
const { data } = useGetPosts();
```
👉 단 한줄 !!!!! 정말 대박이다...!

### 참고
- 킹왕짱상기 매니저님🥺
