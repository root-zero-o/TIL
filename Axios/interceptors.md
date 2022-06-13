# Interceptors

## 1. Interceptor란?
- 인터셉터로 요청하기 직전, 응답을 받고 then이나 catch로 처리하기 직전에 가로챌 수 있음!
- 구성 : 인스턴스, request 설정, response 설정
- axios는 기본적으로 api timeout이 설정되어 있지 않아 API를 호출하면 서버에서 응답주기 전까지 계속 연결되어 있음
```javascript
import axios from 'axios'

/* 1. axios 인스턴스 생성 */
const request = axios.create({
  baseURL : "https://api.com",
  timeout: 30000 //timeout 설정
});

/* request 인터셉터(2개의 콜백함수를 받음) */
instance.interceptors.request.use(
  function (config) {
    // 요청 성공 직전 호출됨
    // axios 설정값을 넣음(사용자 정의 설정 추가 가능)
    return config;
  },
  function (error) {
    // 요청 에러 직전 호출됨
    return Promise,reject(error);
  }
)

/* response 인터셉터(2개의 콜백함수를 받음) */
instance.interceptors.response.use(
  function (response) {
    // http status가 200인 경우 응답 성공 직전 호출됨
    // .then() 으로 이어짐
    return response;
  },
  
  function (error) {
    // http status가 200이 아닌 경우 응답 에러 직전 호출됨
    // .catch()으로 이어짐
    return Promise.reject(error);
  }
)
```

## 2. 예시
<img src="https://user-images.githubusercontent.com/97326130/173282641-1469826b-b532-46de-9161-8e87e3b24a9b.png" width="600"/>

- core 디렉토리에 axios 인스턴스를 생성하는 파일인 ```index.js```를 만듦
- core 밖에 ```main.js```에서 axios 인스턴스를 import한 후, api를 호출하는 함수를 모아놓은 파일


#### /src/api/core/index.js
```javascript
import axios from "axios";

// 1. Axios Instance를 생성
const api = axios.create({
  baseURL: "http://localhost:3001",
});

// 2. 요청 타임아웃 설정
request.defaults.timeout = 2500;  

// 3. 요청 인터셉터
request.interceptors.request.use(
  config => {
  // 요청 보내기 전에 수행할 로직
  return config
  },
  error => {
  // 요청 에러가 발생했을 때 수행할 로직
  return Promise.reject(error);  // error라는 이유로 거부된 Promise 객체 반환(디버깅)
  }
);   

// 4. 응답 인터셉터
request.interceptors.response.use(
  response => {
  // 응답에 대한 로직 작성
  const res = response.data;
  return res
  },
  error => {
    // 응답 에러가 발생했을 때 수행할 로직
    return Promise.reject(error);
  }
);
 
// 5. axios 인스턴스 내보내기
export default request;
```

#### /src/api/main.js
- core의 index.js를 import

```javascript
import request from "./core/index.js";

// GET 요청 (default여서 파라미터 객체 안에 명시해주지 않아도 됨)
const getUserInfo = (aUserId) => {
  return request({`/getUserInfo/${aUserId}`})
}

// POST 요청 
const saveUserInfo = () => {
  request({
    method: "post",
    url: "/user/12345",
    data: {
      firstname: "근영",
      lastName : "김"
    }
  });
}

export default {
  getUserInfo,
  saveUserInfo
}
```

#### 객체에 넣어 관리
```javascript
import axios from "axios";

// Axios Instance를 생성:: 인스턴스를 이용하면 코드 중복을 최소화 할 수 있다.
const api = axios.create({
  baseURL: "http://localhost:3001",
});

// Instance를 생성하고, 여러개의 요청 함수들을 하나의 객체에 넣어서 관리하는 방법도 있습니다!
const apis = {
  getPosts: () => api.get("/posts"),
  addPost: (newPost) => api.post("/posts", newPost),
  deletePost: (postId) => api.delete(`/posts/${postId}`),
};

export default apis;
```

## 참고
- https://pinokio0702.tistory.com/373
- [예상기 매니저님 repo](https://github.com/with-key/hh99_axios_basic)












