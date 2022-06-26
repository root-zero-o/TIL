# Types

## Basic
- 특정 변수 or 상수의 타입을 지정할 수 있고, 사전에 지정한 타입이 아니면 에러 발생
- 에러가 발생하면 컴파일되지 않음 ! (```tsc``` 명령어 입력해서 컴파일 하려고하면 실패)
```typescript
export let count = 0;  // 숫자
count += 1;
count = "문자열"  // 갑자기 문자열이 오면 에러가 난다.

const message : string = "hello world";  // 문자열로 타입 지정

const done : boolean = true;  // 불리언으로 타입 지정

const numbers : number[] = [1, 2, 3];  // 숫자 배열로 타입 지정
const messages : string[] = ["hello", "world"];  // 문자열 배열로 타입 지정

messages.push(1);  // 문자열 배열에 숫자를 넣으려하면 에러가 난다.

let mightBeUndefined : string | undefined = undefined;  // string 또는 undefined 이다.
let nullableNumber : number | null = null;  // number 또는 null이다.

let color: "red" | "orange" | "yellow" = "red";  // color는 red, orange, yellow 중 하나이다.
color = "yellow";
color = "green";  // 에러 발생

```

## 함수
- 파라미터로 어떤 타입을 넣어야하는지 지정
```typescript
function sum( x : number, y : number) : number {   // x는 숫자, y는 숫자, 결과물도 숫자
  return x + y;  
}

sum(1, 2);
```
- 배열 내장함수 사용시에도 타입 유추가 잘 이루어짐
```typescript
function sumArray(numbers: number[]): number {  // 파라미터는 숫자 배열이고, return값은 숫자
  return numbers.reduce((acc, current) => acc + current, 0);
}

const total = sumArray([1, 2, 3, 4, 5]);
```
- 아무것도 반환하지 않아야 할 때
```typescript
function returnNothing(): void {  // return 타입을 void로 설정함
  console.log('I am just saying hello world');
}
```

## 참고
- [벨로퍼트 모던 리액트 - 타입스크립트](https://react.vlpt.us/using-typescript/01-practice.html)
