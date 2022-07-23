# 옵셔널 체이닝(Optional-chaining)

```javascript
let value = elem?.value;
```

- ES11(ECMAScript 2020)에서 도입되었다.
- ```?.``` 좌항의 피연산자가 ```null``` 또는 ```undefined```인 경우 ```undefined```를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어간다.
- 좌항 피연산자가 false로 평가되는 ```Falsy 값```이라도 ```null``` 또는 ```undefined```가 아니면 우항의 프로퍼티 참조를 이어간다.


```javascript
// 논리연산자(&&)를 사용했을 경우
// 좌항 피연산자가 Falsy 값(0이나 "" 등)인 경우도 좌항 피연산자를 그대로 반환한다.

let str = "";

let length = str && str.length;

// 문자열의 길이를 참조하지 못한다.
console.log(length)  // ""
```

```javascript
// 옵셔널 체이닝(?.)을 사용했을 경우
// 좌항 연산자가 Falsy 값(0이나 "" 등)인 경우에도 null 또는 undefined가 아니면 우항의 프로퍼티 참조를 이어간다.
let str = "";

let length = str?.length;
console.log(length);  // 0
```

## 참고
- 모던 자바스크립트 Deep Dive
