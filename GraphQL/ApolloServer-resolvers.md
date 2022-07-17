# Apollo Server로 API 만들기 - Resolvers

### 개념

```javascript
 // resolver
 const resolvers = {
  Query: {
    tweet() {
      console.log("I'm called ");
      return null;
    },
    ping() {
      return "pong";
    },
  },
};

// request
{
  tweet(id:"1") {
    text
  }
  ping
}

// response
{
  "data": {
    "tweet": null,
    "ping": "pong"
  }
}

// 여기에 resolver 넣어주기 !
const server = new ApolloServer({ typeDefs, resolvers });

```
- 타입의 각 필드는 GraphQL 서버개발자가 만든 ```resolver``` 함수에 의해 실행된다.
- 필드가 실행되면 해당 ```resolver```가 호출되어 값을 생성하고, 값을 반환하면 실행이 완료된다.
- 필드가 객체를 반환하면 쿼리는 해당 객체에 적용되는 다른 필드들을 포함하게 되는데, 값에 스칼라 값에 도달할 때까지 반복된다.
- 인수
    - obj : 대부분 사용되지 않는 루트 Query 타입의 이전 객체
    - args : GraphQL 쿼리의 필드에 제공된 인수
    - context : 모든 resolver 함수에 전달되며, 현재 로그인한 사용자, 데이터베이스 액세스와 같은 중요한 문맥 정보를 보유하는 값
    - info : 현재 쿼리, 스키마 정보와 관련된 필드별 정보를 보유하는 값


### Dynamic Field

```javascript
// DB
// DB에는 fullName이 없음
let users = [
  {
    id: "1",
    firstName: "geunyeong",
    lastName: "Kim",
  },
];

// type
// type에는 fullName이 non-nullable fields로 설정됨
type User {
    id: ID!
    firstName: String!
    lastName: String!
    fullName: String!
  }
  
 // resolver
 const resolvers = {
  Query: {
    allUsers() {
      console.log("allUsers called");  //  allUsers()가 먼저 실행된다.
      return users;  // users를 return해야하지만 fullName을 찾을 수 없다.
    },
  },
  User: {
    fullName(root) {
      console.log("fullName called");  // allUsers()가 실행된 후 fullName()이 실행된다.
      console.log(root)  // { id: '1', firstName: 'geunyeong', lastName: 'Kim' } 이 콘솔에 출력됨
      return "hello!";  // 여기서 fullName을 찾아서 return한다.
    },
  },
};

//request 
{
  allUsers {
    id
    firstName
    lastName
    fullName
  }
}

//response
{
  "data": {
    "allUsers": [
      {
        "id": "1",
        "firstName": "geunyeong",
        "lastName": "Kim",
        "fullName": "hello!"  // fullName이 출력됨
      }
    ]
  }
}
```

위의 예시에서 resolver의 인수인 root에 user 정보가 모두 담기는 것을 활용

```javascript
// DB
let users = [
  {
    id: "1",
    firstName: "geunyeong",
    lastName: "Kim",
  },
  {
    id: "2",
    firstName: "Elon",
    lastName: "Mask",
  },
];

// resolver
const resolvers = {
  Query: {
    allUsers() {
      console.log("allUsers called");
      return users;
    },
  },

  User: {
    fullName({ firstName, lastName }) {
      return `${firstName} ${lastName}`;
    },
  },
};

// request
{
  allUsers {
    id
    firstName
    lastName
    fullName
  }
}

// response
{
  "data": {
    "allUsers": [
      {
        "id": "1",
        "firstName": "geunyeong",
        "lastName": "Kim",
        "fullName": "geunyeong Kim"
      },
      {
        "id": "2",
        "firstName": "Elon",
        "lastName": "Mask",
        "fullName": "Elon Mask"
      }
    ]
  }
}
```

## 참고
- 노마드코더 'GraphQL로 영화 API 만들기'
