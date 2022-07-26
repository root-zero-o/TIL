# 튜플(Tuple)

```typescript
let babo : [string, number];

babo = ["rootzero", 25];
babo = [25, "rootzero"];  // Error
```
- 서로 다른 타입을 함께 가질 수 있는 배열
- 요소의 타입과 개수가 고정된 배열을 표현할 수 있다.(단, 요소들의 타입이 모두 같을 필요는 없다.)
- 요소를 선택사항으로 입력할 수 있다.
```typescript
type Tuple = [id: number, name?: string];
```

- spread 연산자를 사용해 나머지를 표현할 수 있다.
```typescript
let foo: [...string[], number];

foo = ["hello!", "hello!", "hello!", 123];
```



## 주의할 점
- 튜플 타입의 값을 Array 프로토타입 메서드를 통해 조작해도 에러는 발생하지 않는다.
```typescript
let babo : [string, number];
babo = ["rootzero", 25];
babo.push(100);  // no error
```

## 참고
- https://typescript-kr.github.io/pages/basic-types.html#%ED%8A%9C%ED%94%8C-tuple
- https://ahnheejong.gitbook.io/ts-for-jsdev/03-basic-grammar/array-and-tuple
- 
