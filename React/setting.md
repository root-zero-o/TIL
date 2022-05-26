# 프로젝트 세팅
## 1. 프로젝트 생성
- nvm 설치
    - [NVM 설치 파일 다운로드 링크](https://seunghyun90.tistory.com/52) 에 들어가서 ```nvm-setup.zip``` 다운받기
    - 압축 파일을 풀고 nvm 설치
- nvm 설치 확인(VSCode 터미널)
```
nvm --version // 설치한 nvm 버전 확인
```
- Node.js에서 최신버전 확인 후 설치하기
```
nvm install [설치할 버전]
```
```
nvm ls // nvm으로 설치한 노드 버전 리스트 확인 명령어
node -v // 노드 버전 확인 명령어
node use [사용할 노드 버전] // 사용 중인 노드 버전 바꾸기
```
*exit status 1, status5 오류 뜨면 ? PowerShell 관리자모드로 켜고 nvm use 쓰면 됨!*

- npm으로 yarn 설치
```
npm install -g yarn // npm으로 yarn을 컴퓨터 전체에 설치
```
- yarn으로 패키지 설치
```
yarn add [옵션] [패키지 이름]
```
- CRA 설치
```
yarn add global create-react-app
```
- 리액트 프로젝트 만들기
```
yarn create react-app [프로젝트 이름]
```
- 프로젝트 실행
```
cd [프로젝트 이름] // 폴더로 이동
yarn start
```

## 2. 폴더 정리
### 1) ```public```폴더
- index.html 파일 외의 기타 파일 삭제
- index 파일 코드 정리
```html
 <!DOCTYPE html>
  <html lang="ko">   // 1. 한국 사이트니까 당연히 setting
    <head>
      <meta charset="utf-8" />
      <title>React App</title>    // 2. title 설정
    </head>
    <body>
      <div id = "root"></div>    // 3. root id 담긴 div 구조는 남겨야함
    </body>
  </html>
```
### 2) ```src``` 폴더 
- index.js / App.js 파일 외 기타 파일 삭제
```javascript
function App() {
   return (
     <div>
       // ...
     </div>
   );
 }

 export default App;
```

## 참고
- [윤님의 TIL](https://github.com/kordobby/amazon/blob/main/React/react_guideline/react_basic.md)
