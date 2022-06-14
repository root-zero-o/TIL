# 🛠Settings🛠

### 1. 설치
```
yarn add react-query  // yarn
npm i react-query  // npm
```

### 2. App.js
```javascript
// 1. import 
 import {
   useQuery,
   useMutation,
   useQueryClient,
   QueryClient,
   QueryClientProvider,
 } from 'react-query'  
 
 // 2. Create a client
 const queryClient = new QueryClient()
 
 function App() {
  return (
    // 3. Provide the client to App
     <QueryClientProvider client={queryClient}>
       <Todos />
      </QueryClientProvider>
  )
}
```

### 참고
- [React query 공식문서](https://react-query.tanstack.com/quick-start)
