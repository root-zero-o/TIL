# ```var```,```let```,```const``` 비교



## 1. ```var```
- 함수 레벨 스코프 : 함수의 코드 블록만을 지역 스코프로 인정 👉 의도치 않게 전역변수가 중복 선언됨
```javascript
var x = 1;

if(true){
  var x = 10;  // x가 중복선언된다.
}

console.log(x); // 10
```
- ```var```을 사용하여 재선언(re-declare)이 가능하며, var 변수를 업데이트할 수 있음
- 변수 호이스팅에 의해 변수 선언문이 스코프의 선두로 끌어 올려진 것처럼 동작함
```javascript
console.log(x);  // undefined

x = 123;

console.log(x);  // 123

var x;  // 변수 선언은 JS 엔진에 의해 런타임 이전에 암묵적으로 실행됨
```
- var 키워드로 선언한 전역 변수, 전역 함수, 암묵적 전역(선언하지 않은 변수에 값을 할당함)은 전역객체 window의 프로퍼티가 됨

<br/>

## 2. ```let```
- 블록 레벨 스코프 : 모든 코드 블록(함수, if문, for문, while문, try/catch문 등)을 지역 스코프로 인정
```javascript
let a = 10
  if(true) {
    let a = 9
    let b = 0
    console.log(a) // 9
  }
console.log(a) // 10
console.log(b) // ReferenceError
```
- 변수중복선언은 할 수 없으나, 변수 값을 재할당할 수는 있음
```javascript
let a = 10
let a = 8 // not allowed
a = 8 // allowed
console.log(a) // 8
```
- let 키워드로 선언한 변수는 변수 호이스팅이 발생하지 않는 것처럼 동작함
    - var : 런타임 이전에 자바스크립트 엔진에 의해 암묵적으로 ```'선언 단계'와 '초기화 단계'가 한번에 진행됨```
    - let : ```'선언 단계'와 '초기화 단계'가 분리되어 진행됨```(런타임 이전에 선언 단계 실행, 변수 선언문에 도달했을 때 초기화 단계 실행)
    - 초기화 단계가 실행되기 전에 변수에 접근하려 하면 참조 에러 발생
    - 스코프 시작 지점부터 초기화 시작 지점까지 변수를 참조할 수 없는 구간을 ```일시적 사각지대(TDZ : Temporal Dead Zone)```라고 함
- let 키워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 아님(전역 렉시컬 환경의 선언적 환경 레코드 내에 존재함)

<br/>

## 3. ```const```
- const 키워드로 선언한 변수는 반드시 선언과 동시에 초기화해야 한다.
```javascript
const x = 1;

const y;  // SyntaxError
```
- ```let```과 비슷하지만, 변수를 재선언하거나 재할당할 수 없음
```javascript
const name = 'yeong'
console.log(name) 
// yeong

const name = 'babo'
console.log(name) 
// Uncaught SyntaxError: Identifier 'name' has already been declared

name = 'babo'
console.log(name) 
//Uncaught TypeError: Assignment to constant variable.
```
- 블록 레벨 스코프, 변수 호이스팅이 발생하지 않는 것처럼 동작함
- const 키워드로 선언한 변수에 원시 값을 할당한 경우 변수 값을 변경할 수 없음 👉 ```상수를 표현하는 데 사용```
- const 키워드로 선언된 변수에 객체를 할당한 경우 값을 변경할 수 있음

## 5. 결론
- 변수 선언에는 기본적으로 ```const```를 사용하고, 재할당이 필요한 경우에 한정해 ```let```을 사용


## 참고사이트
- 모던 자바스크립트 Deep 
- https://www.geeksforgeeks.org/difference-between-var-let-and-const-keywords-in-javascript/
- https://velog.io/@bathingape/JavaScript-var-let-const-%EC%B0%A8%EC%9D%B4%EC%A0%90
- https://gist.github.com/LeoHeo/7c2a2a6dbcf80becaaa1e61e90091e5d
