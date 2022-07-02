# CSR, SSR, SSG 알아보기

## 1. CSR(Client Side Rendering)
![173243095-fb985d43-3e98-47c5-b92e-27745cba1e71](https://user-images.githubusercontent.com/97326130/176996336-71b211f2-ba0d-4876-94cc-f1cb9000fc1f.png)
### 특징
- JS, CSS를 ```index.js```, ```index.css```와 같이 하나의 파일로 번들링
- 페이지 요청 시 서버는 빈 HTML과 ```index.js```, ```index.css```를 제공함 👉 브라우저에서 JS와 CSS를 분석해 페이지 렌더링
- JS나 CSS의 요청을 한 번만 수행하면 됨 👉 SPA를 구현하는 데 매우 용이함
### 장점
- 페이지 이동에 발생하는 깜빡임 현상 제거, 빠르고 자연스러운 페이지 렌더링
- 서버의 부담이 적음
### 단점
- 번들링 파일의 용량이 매우 크기 때문에 페이지 초기 호출이 지연됨
- SEO에 취약함(렌더링 이전엔 빈 HTML만 표시하기 때문)

## 2. SSR(Server Side Rendering)

![173243156-48c774f4-5080-4cd4-85f6-0bb900655b47](https://user-images.githubusercontent.com/97326130/176996492-b185fb8d-225f-420f-ab4b-29784ff8015b.png)
### 특징
- 각 URL마다 서버가 요청을 받아, 정의된 로직에 따라 페이지를 렌더링하는 방식
- 브라우저는 서버에서 제공한 파일을 그대로 표시하고 스크립트를 수행하는 역할만을 수행
### 장점
- 초기 로딩이 CSR에 비해 빠름
- 브라우저가 응답 받는 시점에 이미 기본적인 렌더링이 완료된 상태이므로, SEO에도 유리함
- 사용자 디바이스에 상관없이 비교적 일정한 퍼포먼스 제공
### 단점
- 페이지 요청시 서버에 부담
- CSR은 단순 라우팅 서버만으로 구현이 가능하나, SSR은 직접 컨트롤 가능한 서버를 요구함(경제적 비용 야기)

## 3. SSG(Static Site Generator)
![173244087-8061b020-3aba-48b8-95bd-4e698efbfb01](https://user-images.githubusercontent.com/97326130/176996665-3f7d9be4-1b7e-4def-9367-27d299bea412.png)
### 특징
- 각 페이지의 HTML, JS, CSS를 빌드하여 URL별 파일 생성
- 이미 파일이 정의되었기 때문에 기능이 제한적임
- 빌드 시 이미 렌더링된 페이지 자체를 아예 빌드함 👉 CSR, SSR 모두 SSG로 빌드해 운용이 가능함

## 참고
- https://blog.itcode.dev/posts/2022/06/12/csr-ssr-ssg
- https://velog.io/@altmshfkgudtjr/CSR-SSR-SSG-%EC%A1%B0%ED%99%94%EB%A5%BC-%EC%9D%B4%EB%A3%A8%EB%8B%A4








