# Apollo Client - useMutation 사용하기

- 렌더링될 때 자동으로 실행되는 ```useQuery```와 달리, ```useMutation```은 수동으로 실행해주어야 한다 !
- Apollo Client는 기본적으로 서버에서 받아온 값을 ```Apollo Cache에 자동으로 저장```한다.
- 따라서 서버의 값이 업데이트 되어도, Cache에 저장된 값은 그대로이기 때문에 ```새로고침을 해야 변화가 반영된다```.
- 이러한 문제를 ```refetchQuery```, ```cache.modify```의 두 가지 방법으로 해결할 수 있다.

----

## DB 업데이트

### 1. mutation 작성
```graphql
const ADD_TODO = gql`
  mutation ($text: String!) {   // 서버에서 정한 type과 동일하게 해주어야 한다.
    addTodo(text: $text) {      
      id                        // 작업이 끝난 뒤 return 되는 값
      text
      done
      location
    }
  }
`;
```

### 2. mutation 함수 꺼내주기

```typescript
const [addTodo, { data, loading, error }] = useMutation(ADD_TODO)

// useQuery와 다르게, 배열로 값들을 꺼내준다.
// 위의 예시에서는 mutation 함수, 작업이 끝나고 return되는 data, loading, error를 꺼내주었다.
```

### 3. mutation 실행

```typescript
const onSubmit = (e: React.FormEvent<HTMLFormElement>) => {
    e.preventDefault();
    addTodo({ variables: { text: input } });  // 꺼내준 함수에 필요한 인자를 넘겨주어 실행한다.
    setInput("");
    alert("추가완료!");
  };
```

-----

## DB 업데이트 후 cache 업데이트
### 1. refetchQuery

- mutation 함수 실행이 끝난 후 서버에서 다시 필요한 값을 받아오는 직관적인 방법
- 하지만 서버와의 통신이 추가적으로 발생한다는 단점이 있다.

```typescript
const DELETE_TODO = gql`
  mutation deleteTodo($deleteTodoId: String!) {
    deleteTodo(id: $deleteTodoId)
  }
`;

  const [deleteTodo] = useMutation(DELETE_TODO, {
    refetchQueries: [{ query: GET_TODOS }, "getTodos"], // useMutation의 두 번째 인자로 refetchQueries 사용
                                                        // useQuery로 값을 불러왔던 함수와 동일한 이름을 사용해야 한다.
  });
  const onClick = async () => {
    try {
      await deleteTodo({
        variables: { deleteTodoId: String(id) },  
      });
      alert("삭제 완료!");
    } catch (error) {
      alert("error!");
    }
  };
```

### 2. cache.modify

- 서버와의 통신 없이 직접 cache에 저장된 값을 수정하는 방법
- mutation이 복잡해진다는 단점이 있다.

```typescript
const ADD_TODO = gql`
  mutation ($text: String!) {
    addTodo(text: $text) {
      id
      text
      done
      location
    }
  }
`;

const [addTodo, { loading, error }] = useMutation(ADD_TODO, {
    update(cache, { data: { addTodo } }) {  // mutation 실행이 끝나고 return되는 data
      cache.modify({
        fields: {
          // 모든 데이터를 불러오는 함수명을 알맞게 적어주어야 한다.(allTodos)
          allTodos(oldTodos = []) {  
            const newTodoRef = cache.writeFragment({
              data: addTodo,
              fragment: gql`
                fragment NewTodo on Todo {
                  id
                  text
                  done
                }
              `,
            });
            return [...oldTodos, newTodoRef];
          },
        },
      });
    },
  });
```

----

## 참고
- https://www.apollographql.com/docs/react/caching/cache-interaction/
