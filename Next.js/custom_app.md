# Custom App

- 서버로 요청이 들어왔을 때 가장 먼저 실행되는 컴포넌트
- 페이지에 적용할 공통 레이아웃 역할, 모든 컴포넌트에 공통으로 적용할 속성 관리(global CSS)
- server only file : client에서 사용하는 로직(eventlistener 등 window/DOM 로직)은 사용 불가
- 파일 이름 :  ```_app.js```

## 1. 형태
```javascript
function MyApp({ Component, pageProps }) {
  return <Component {...pageProps} />
}

export default MyApp
```
- ```Component``` : 서버에 요청한 페이지
- ```pageProps``` : ```getInitialProps```, ```getStaticProps```, ```getServerSideProps``` 중 하나를 통해 페칭한 초기 속성값
- ```getInitialProps```를 사용해 모든 페이지에서 사용할 공통 속성값 지정 가능 (but 모든 페이지가 서버 사이드 렌더링을 통해 제공됨)

## 2. ServerSide Cycle
1. Next Server가 GET 요청을 받음
2. 요청에 맞는 page를 찾음
3. ```_app.js```의 ```getInitialProps```가 있다면 실행하고, pageProps들을 받아옴
4. ```_document.js```의 ```getInitialProps```가 있다면 실행하고, pageProps들을 받아옴
5. 모든 props들을 구성하고 ```_app.js``` > page Component 순서로 렌더링함
6. 모든 Content를 구성하요 ```_document.js```를 실행해 html형태로 출력



## 참고
- https://nextjs.org/docs/advanced-features/custom-app
- https://merrily-code.tistory.com/154
- https://velog.io/@cyranocoding/Next-js-%EA%B5%AC%EB%8F%99%EB%B0%A9%EC%8B%9D-%EA%B3%BC-getInitialProps
