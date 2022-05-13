## ```isNaN()```함수로 문자열이 숫자인지 체크하기

### 구문
```javascript
isNaN(value)
```
- 파라미터 : 테스트할 값 입력
- 리턴값 : 파라미터가 숫자가 아닐 경우(```NaN```) true, 숫자일 경우 false 리턴

### 예제
```javascript
console.log(isNaN(123)); // false
console.log(isNaN(-22)); // false

console.log(isNaN("babo")); // true
console.log(isNaN(undefined)); // true
console.log(isNaN()); // true
console.log(isNaN(null)); // true
```

### 참고
- https://hianna.tistory.com/385
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/isNaN
