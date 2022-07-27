# 제네릭(Generic)

## 정의
- 타입 정보가 동적으로 결정되는 타입
- 타입에 유연성을 제공하여 컴포넌트 등에서 재사용을 가능하게 해주는 타입
- 타입을 마치 함수의 파라미터처럼 사용하게 해준다.

```typescript
function getText<T>(text: T): T {
  return text;
}

// T는 유저가 준 인수의 타입을 캡처하고 다시 사용한다.
// 입력 값의 타입이 string 이면서 반환 값의 타입도 string이어야 한다.
// 여기서 T는 제네릭을 선언할 때 관용적으로 사용되는 식별자로 타입 파라미터(Type parameter)라 한다.
```

## 제네릭 제약조건(Generic Constraints)
- 타입이 무엇이 될 수 있는지에 대한 제약조건
- ```extends``` 키워드를 통해 명시한다.

```typescript
interface Lengthwise {
  length: number;
}

function loggingIdentity<Type extends Lengthwise>(arg: Type): Type {
  console.log(arg.length);  // 오류가 나지 않는다.
  return arg;
}
```

- keyof 사용
```typescript
function getProperty<Type, Key extends keyof Type>(obj: Type, key: Key) {
  return obj[key];
}
 
let x = { a: 1, b: 2, c: 3, d: 4 };
 
getProperty(x, "a");
getProperty(x, "m");  // Error, "a" | "b" | "c" | "d" 에 속하지 않는다.
```

## extension

- 삼항연산자 사용

```typescript
interface Post {
  v:string;
}

interface Comment {
  m:string;
}

interface Board<T>{
  getItem(): T extends Post ? Post : Comment
}
```

- JSX arrow function
HTML태그가 아니라 제네릭이라는 힌트를 주기 위해 ```extends {}```를 사용한다.

```typescript
const foo = <T extends unknown>(x: T) => x;
```


## 참고
- https://joshua1988.github.io/ts/guide/generics.html
- https://www.typescriptlang.org/docs/handbook/2/generics.html
- https://poiemaweb.com/typescript-generic
- https://velog.io/@edie_ko/TypeScript-Generic-%EC%A0%9C%EB%84%A4%EB%A6%AD-feat.-TypeScript-%EB%91%90-%EB%8B%AC%EC%B0%A8-%ED%9B%84%EA%B8%B0
