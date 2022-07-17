# GraphQL이란?

## 1. GraphQL(Graph Query Language) ?
### 개념
- Facebook에서 만든 어플리케이션 레이어 쿼리 언어
- 웹 클라이언트가 데이터를 서버로부터 효율적으로 가져오는 것이 목적
- 타입 시스템을 사용하여 쿼리를 실행하는 서버사이드 런타임
- 특정 데이터베이스나 스토리지에 귀속되어 있지 않으며, 기존 코드와 데이터에 의해 대체됨

### 작동방식
- 클라이언트에서 사용할 Query Language를 정의함
- 클라이언트가 자신에게 필요한 데이터에 대한 Query를 선언해 GraphQL에 넘기면, GraphQL은 Query를 해석해 서버에서 필요한 데이터를 가져온 후 클라이언트에 해당 쿼리에 대한 데이터를 반환한다.

![화면 캡처 2022-07-17 174500](https://user-images.githubusercontent.com/97326130/179390916-81f0d2e2-f182-4c07-9d14-638d9a824529.png)
*이미지 출처 : https://kotlinworld.com/330*

## 2. GraphQL을 사용하는 이유
### Over-fetching
- REST API
```javascript
GET /user/1/
response body
{
"user_no":1,
"user_name": "test",
"user_grade": "VVIP",
"zip": "11053",
"last_login_timetamp": "2019-08-08 12:11:44",
...
}
```
    - 위의 API에서, 클라이언트가 유저의 이름만 얻고 싶어도 모든 데이터를 다 받아서 사용해야 한다.
    - 이렇게 사용하지 않는 데이터까지 넘치게 받는 것을 Over-fetching이라 한다.
- GraphQL
```javascript
// request
query{
      user(user_no:1){
            user_name  
      }
}

// response(JSON)
{
      "data": {
            "user": {
                  "user_name": "jim",
            }
      }
}
```
    - GraphQL을 사용하면 내가 원하는 데이터만 받을 수 있다.

### Under-fetching
- REST API
```
/user/1/
/cart/
/notification/
/wish/
...
```
    - 로그인한 사용자의 장바구니 정보를 보여주는 경우, 데이터를 얻기 위해 여러 API를 호출해야 한다.
    - 요청에 맞는 유효한 데이터를 보여주기 위해 여러 API를 호출하게 되는 경우를 Under-fetching이라 한다.

- Graph QL
```javascript
// request
{
  human(id: "1000") {
    name
    height(unit: FOOT)
  }
}

// response(JSON)
{
  "data": {
    "human": {
      "name": "Luke Skywalker",
      "height": 5.6430448
    }
  }
}
```
    - 객체의 인자를 통해 한 번의 요청으로 데이터를 가져올 수 있다.

*GraphQL 맛보기 : https://graphql.org/swapi-graphql* 

## 참고
- 노마드코더 'GraphQL로 영화 API 만들기'
- https://graphql-kr.github.io/learn/
- https://hanamon.kr/graphql%EC%9D%B4%EB%9E%80-api%EB%A5%BC-%EC%9C%84%ED%95%9C-%EC%BF%BC%EB%A6%AC-%EC%96%B8%EC%96%B4/
- https://kotlinworld.com/330


