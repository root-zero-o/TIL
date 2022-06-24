# Pre-rendering

## Pages

- Next.js는 ```pages``` 디렉토리 안의 ```.js```, ```.jsx```, ```.ts```, ```.tsx``` 파일들은 파일 이름으로 route 됨
- ```pages/posts/[id].js```라는 파일은 ```/posts/1```, ```posts/2``` 등 으로 접근할 수 있음
- src/pages/about.js (파일 명 = url)
```javascript
export default function Potato(){   // export default로 작성, 컴포넌트 이름은 중요X
  return "Hi";
}
```
- 파일명이 ```index.js```이면 홈페이지
- jsx를 사용하면 react를 import할 필요가 없음

## Pre-rendering
### 1. 개념
- Client-side Rendering
    - 일반적인 react의 방식. HTML을 빈 div로 불러오고, 모든 자바스크립트 코드를 불러온 뒤 화면에 표시
    - 인터넷이 느리면 자바스크립트 코드를 불러오기 전까지 *흰 화면*이 보임 :(
- Next.js는 모든 페이지(HTML)를 pre-render함!
- HTML을 먼저 표시해준 뒤, 데이터를 표시해줌

### 2. 방식
- Static Generation : HTML을 빌드타임에 생성해 두고 요청시마다 재사용하는 방법 
- Server-Side Rendering : 요청시마다 HTML을 생성해주는 방법 <br>
*각 페이지마다 방식을 선택할 수 있음 !*

### 3. Static Generation
>#### data fetching이 필요하지 않은 경우

- Next.js는 빌드 타임에 페이지마다 HTML 파일을 만듦
    
>#### data fetching이 필요한 경우
- page content가 외부 데이터에 의존할 경우 : ```getStaticProps```를 사용
```javascript
function Blog({ posts }) {
}

// 빌드타임에 call됨
export async function getStaticProps() {

  const res = await fetch('https://.../posts')
  const posts = await res.json()

  // By returning { props: { posts } }, the Blog component
  // will receive `posts` as a prop at build time
  return {
    props: {
      posts,
    },
  }
}

export default Blog
```
- page paths가 외부 데이터에 의존할 경우 : ```getStaticPaths``` 사용
```javascript
// 빌드타임에 call될 함수
export async function getStaticPaths() {

  const res = await fetch('https://.../posts')
  const posts = await res.json()

  const paths = posts.map((post) => ({
    params: { id: post.id },
  }))

  // We'll pre-render only these paths at build time.
  // { fallback: false } means other routes should 404.
  return { paths, fallback: false }
}
```
받아온 id에 맞는 테이터를 fetch하고, 이 페이지를 pre-render하기 위해서는 ```getStaticProps``` 사용
```javascript
function Post({ post }) {
  // Render post...
}

export async function getStaticPaths() {
  // ...
}

// This also gets called at build time
export async function getStaticProps({ params }) {
  // params contains the post `id`.
  // If the route is like /posts/1, then params.id is 1
  const res = await fetch(`https://.../posts/${params.id}`)
  const post = await res.json()

  // Pass post data to the page via props
  return { props: { post } }
}

export default Post
```

### 4. 🤷‍♀️ Static Generation 왜 사용해?
- 모든 요청에 대해 server render를 하는 것보다 더 빠르기 때문에 !
- 언제 쓸까 ?
사용자의 요청보다 더 먼저 pre-render를 하고싶을 때
- 언제 쓰지 말까 ?
    - 페이지에서 수시로 업데이트되는 데이터를 보여줄 때
    - 페이지의 내용이 매 요청마다 달라질 때
👉 이럴 땐 Server-side Rendering 을 사용하거나, 부분적으로 Client-side Rendering을 사용하자 !
    
### 5. Server-side Rendering(Dynamic Rendering)
- 페이지의 HTML은 매 요청마다 만들어짐
- ```getServerSideProps()```를 사용해야 함(*매 요청마다 서버에 의해 call됨*)
```javascript
function Page({ data }) {

}

// 매 요청마다 call됨
export async function getServerSideProps() {

  const res = await fetch(`https://.../data`)
  const data = await res.json()

  // props를 통해 받아온 데이터를 넘겨준다
  return { props: { data } }
}

export default Page
```

## 참고
- https://nextjs.org/docs/basic-features/pages
