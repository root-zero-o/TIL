# 오버로드(overload)

## 왜 쓰나요🤔
- 다른 타입의 인수를 허용하는 함수를 작성할 때, 보통 Union 타입을 많이 사용한다.
```typescript
function foo(a: string | number) {
  if (typeof a === 'string') {
    // do something...
  }

  if (typeof a === 'number') {
    // do something...
  }
}
```
- 이 때, 인수가 어떤 타입이느냐에 따라 리턴 타입이 달라진다고 하면, Union 타입으로는 명확히 나타낼 수 없다.

```typescript
function switchIt<T extends string | number>(
  input: T,
): T extends string ? number : string {
  if (typeof input === 'string') {
    return Number(input) as string & number
  } else {
    return String(input) as string & number
  }
}

const num = switchIt('1') // has type number ✅
const str = switchIt(1) // has type string ✅
```
- 함수 오버로드를 사용하면 인수 타입에 따라 달라지는 리턴 타입을 명확히 나타낼 수 있다.

<br>

## 그래서 오버로드가 뭐죠🤔

- 인자가 다르고 함수명이 동일한 것을 ```오버로딩 함수```라고 부른다.
- 오버로드 함수를 정의할 때는 순서를 지켜야 한다.
- 오버로딩 방식 타이핑 과정 : call signature 만들기 👉 구현부 작성(인수 타입 받기, 타입 가드 사용해 적절한 처리)
- 위의 예시를 오버로드 방식으로 바꾸기

```typescript
// call signature
function switchIt_overloaded(input: string): number  // 인수 타입에 따른 리턴 타입 명시
function switchIt_overloaded(input: number): string

// 구현부
function switchIt_overloaded(input: number | string): number | string {  // 인수 타입 명시
  if (typeof input === 'string') {  // 타입 가드 사용해 적절한 처리
    return Number(input)
  } else {
    return String(input)
  }
}
```
- 가독성 향상, 리턴 타입 명시

<br>

## 주의할 점
```typescript
function switch_overloaded(input: string): number  // 인수 타입이 string일 때, 리턴 타입 number
function switch_overloaded(input: number): string  // 인수 타입이 number일 때, 리턴 타입 string
function switch_overloaded(input: number | string): number | string {
  if (typeof input === 'string') {  // 인수 타입 string일 때 
    return input // 그냥 string 리턴함
  } else {  // 인수 타입 number일 때 
    return input // number 리턴함
  }
}

const num = switch_overloaded('1') // 에러가 나지 않는다.
const str = switch_overloaded(1) // 에러가 나지 않는다.
```
> 타입스크립트 컴파일러는 함수 본체의 코드 (오버로드 된)의 함수 시그니처와 대조할 뿐이지, 분기 문에서 어떻게 오버로드를 다루는지는 알 수 없다. 결과적으로, 오버로드 함수 시그니처와 모순된 내부 코드를 작성할 수 있는 위험성이 존재한다.

<br>

## 참고
- https://yceffort.kr/2022/03/polymorphic-function-in-typescript#%ED%95%A8%EC%88%98-%EC%98%A4%EB%B2%84%EB%A1%9C%EB%93%9C
- https://velog.io/@ssswon/TypeScript-overLoading



