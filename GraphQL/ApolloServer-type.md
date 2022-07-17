# Apollo Server 만들기 - type

## type?
- schema definition language
- data의 shape을 미리 Apollo Server에 알려준다.
- R은 ```Query```에 넣어주고, CUD는 ```Mutation```에 넣어준다.(여기서 type Query는 필수 !)
```javascript
// server.js
const typeDefs = gql`
  type User {
    id: ID
    username: String
  }
  type Tweet {
    id: ID
    text: String
    author: User
  }
  
  type Query {
    allTweets: [Tweet]  
    tweet(id:ID): Tweet  
  }
  type Mutation {
    postTweet(text:String, userId : ID): Tweet
    deleteTweet(id: ID): Boolean
  }
`;
```

### Mutation
- 위의 예시에서 postTweet은 ```Argument```로 text, userId를 가진다. (postTweet을 호출할 때 text와 userId를 보내야한다.)
- 호출 후 Tweet 타입에 해당하는 id, text, author를 받는다. <br><br>
![화면 캡처 2022-07-17 194958](https://user-images.githubusercontent.com/97326130/179394841-0c2c7932-fbab-4399-8c46-a64db3f7b68d.png) <br>
*(Apollo studio에서 위와 같이 나타난다.)*
- ```mutation```을 호출할 때는 query와 다르게 앞에 mutation을 붙여줘야 한다.(query는 default라서 앞에 query를 안붙여도 된다.)
```javascript
mutation{
  postTweet(text: "Hello, first tweet", userId: "1") {
    text
  }
}
```

## 참고
- 노마드코더 "GraphQL로 영화 API 만들기"
