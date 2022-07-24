# Apollo Client - useQuery 사용하기

React-query의 useQuery와 동일한 방식으로 사용하면 된다.

### 모든 데이터 가져오기

1. query 작성해주기
```graphql
export const GET_TODOS = gql`
  query getTodos {  # getTodos : 쿼리 이름
    allTodos {      # allTodos : 서버 스키마에서 정한 필드 이름
      id            # 가져올 데이터를 선택해서 적어준다.
      text
      done
    }
  }
`;
```

2. 불러온 데이터 꺼내주기

```typescript
// data와 loading, error를 꺼내준다.
const { data, loading, error } = useQuery(GET_TODOS);  

// 사용할 데이터 가공(type 빼먹지 말기)
const todos: Todo[] = data?.allTodos;

// loading, error 상태에 맞게 다른 렌더링
if (loading) {
    return <h1>loading...</h1>;
  }
  if (error) {
    return <h1>error!</h1>;
  }
```

-----

### 인수에 맞는 데이터 가져오기

1. query 작성해주기

```graphql
const GET_TODO = gql`
  query getTodo($todoId: String!) {  # 인수의 타입을 정해준다.(서버에서 정한 type과 동일해야 한다.)
    todo(id: $todoId) {               # 인수를 정해준다.(스키마에서 정한 인수 이름과 동일해야 한다.)
      id                              # 필요한 데이터를 꺼내준다
      text
      done
      location
    }
  }
`;
```

2. 불러온 데이터 꺼내주기

```typescript
  const { id } = router.query;  // 인수로 줄 id 값을 params에서 가져옴
  const { data, loading, error } = useQuery(GET_TODO, {
    variables: {
      todoId: id,  // 인자를 넘겨준다. variables 안에 객체 형태로 넘겨야 한다.
    },
  });

// 상태에 따라 다른 렌더링
  if (loading) {
    <h1>loading...</h1>;
  }
  if (error) {
    <h1>error</h1>;
  }
```
