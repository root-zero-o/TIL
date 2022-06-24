# Routing

## 1. 정적 라우팅
- 사전에 지정된 주소로 이동하는 방법
- react-router-dom처럼 ```Link``` 컴포넌트를 사용해 주소를 이동할 수 있음
```javascript
import Link from "next/Link";

export default function App() {
  return (
    <div>
      <h2>Link to 'User' Page</h2>
      <Link href="/user">
        <a>move to user</a>
      </Link>
    </div>
  );
}
```
- ```Link```컴포넌트로 감싼 요소를 클릭하면 지정한 경로로 이동
- 컴포넌트를 감쌀 때에는 라우팅이 이루어지지 않음 !
- 브라우저의 ```History API```를 지원함 : 뒤로가기를 하더라도 이전에 렌더링한 페이지를 불러옴(요청X)

<br>

## 2. router 객체
- ```useRouter``` 훅을 통해 사용 가능
- ```router.push()```
```javascript
router.push(url, as, options)
```
> - ```url``` : navigate해서 갈 url 주소
> - ```as``` : 브라우저에서 실제로 보여질 경로
> - ```options```
>     - ```scroll``` : navigation이 이루어진 후에 스크롤이 위로 가도록 함(default : true)
>     - ```shallow``` : Update the path of the current page without rerunning


```javascript
import Link from "next/link";
import { useRouter } from "next/router";

const NavBar = () => {

    const router = useRouter();
    console.log(router)  // location에 대한 정보가 나온다 !
    return (
        <nav>
        <Link href="/">
            <a style={{color: router.pathname === "/" ? "red" : "blue"}}>Home</a>
            // 현재 경로를 router.pathname 으로 가져온 뒤 삼항연산자 사용
        </Link>
        <Link href="/about">
            <a style={{color: router.pathname === "/about" ? "red" : "blue"}}>About</a>
        </Link>
    </nav>
    )
}

export default NavBar;
```
<br>

- router 객체를 통해 routing하기
```javascript
import { useRouter } from "next/router";

export default function App() {
  const router = useRouter();
  return (
    <div>
      <h2>Link to 'tomato' Page</h2>
      <button onClick={() => router.push("/tomato")}>토마토로 가기</button>
      // 함수 내에서 라우팅을 하기 위해서는 라우터 객체 활용
    </div>
  );
}
```
> - ```router.back()``` : 직전 페이지로 돌아가기
> - ```router.push("url")``` : 지정한 경로로 이동하며 히스토리 스택에 URL 추가
> - ```router.replace("url")``` : 지정한 경로로 이동하나 히스토리 스택에 URL 추가하지 않음

<br>

## 3. 동적 라우팅
```javascript
const router = useRouter();
  const onClick = (id) => {
    router.push(`/movies/${id}`);
  };
  
  return (
    <div className='container'>
      <Seo title='Home' />
      {results?.map((movie) => (
        <div
          onClick={() => onClick(movie.id)}
          className='movie'
          key={movie.id}
        >
          ...
        </div>
      ))}
    </div>
  );
```
- URL로 state 넘기기
```javascript
const onClick = (id, title) => {
    router.push(
      {
        pathname: `/movies/${id}`, 
        query: {
          title,  // 직접 접근하거나 새로고침 하는 경우 데이터가 존재하지 않음(처리필요)
        },
      },
    );
  };
```
- ```as```를 사용해 URL 마스킹하기
```javascript
const onClick = (id, title) => {
    router.push(
      {
        pathname: `/movies/${id}`,
        query: {
          title,
        },
      },
      `/movies/${id}`  // 이 부분에서 URL 마스킹
    );
  };
```

*❗ SEO에 영향을 미치는 크롤러는 ```router.push()```가 다른 페이지로 이동하는 링크라고 인식하지 않음*

## 참고
- https://nextjs.org/docs/api-reference/next/router#userouter
- https://gyyeom.tistory.com/64
- 노마드코더 'next.js 시작하기'
