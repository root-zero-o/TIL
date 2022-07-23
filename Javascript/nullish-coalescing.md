# null 병합 연산자(nullish coalescing)

```javascript
let babo = null ?? "babo";
console.log(babo);  // "babo"
```

- ES11(ECMAScript 2020)에서 도입되었다.
- 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 반환한다.
- 변수에 기본값을 설정할 때 유용하다.

- 논리연산자(||) 사용하는 경우
```javascript
// 좌항이 Falsy 값("", 0 등)일 경우 우항의 피연산자를 반환한다.

let babo = "" || "babo"
console.log(babo);  // "babo"
```
- null 병합 연산자(??) 사용하는 경우
```javascript
// 좌항이 Falsy 값("", 0 등)일 경우에도 null, undefined가 아니기 때문에 좌항의 피연산자를 반환한다.
let babo = "" ?? "babo";
console.log(babo);  // ""
```

## 참고
- 모던 자바스크립트 Deep Dive
