# Apollo Server 만들기 - Setting

- node repository 초기화
```
npm init -y
```

- apollo client, graphQL 설치
```
npm i apollo-server graphql
```
- nodemon 설치
```
npm i nodemon -D
```
    - server.js 파일을 저장할 때마다 nodemon이 서버를 재시작
- 파일만들기
```
touch server.js
touch .gitignore
```
- gitignore
```
node_modules/
```
- git 초기화
```
git init .
```
- package.json - script 부분 바꿔주기
```json
{
  "name": "tweetql",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "dev": "nodemon server.js"  // 여기서 명령어 입력
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "apollo-server": "^3.10.0",
    "graphql": "^16.5.0"
  },
  "devDependencies": {
    "nodemon": "^2.0.19"
  },
  "type": "module"  // 타입을 module로 설정(import문 사용)
}
```
- server.js 에서 import
```javascript
import { ApolloServer, gql } from "apollo-server";
```
- type Query 적어주기
```javascript

// schema definition language
// data의 shape을 미리 Apollo Server에 알려준다.
// Query type은 필수
const typeDefs = gql`
  type Query {
    text: String
  }
`;

const server = new ApolloServer({ typeDefs });

server.listen().then(({ url }) => {
  console.log(`Running on ${url}`);
});

```

- 실행
```
npm run dev
```

## 참고 
- 노마드코더 'GraphQL로 영화 API 만들기'
