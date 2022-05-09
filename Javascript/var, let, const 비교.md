## ```var```,```let```,```const``` 비교


### 1. ```var```
-Scope : Global scoped or function scoped
- ```Var```을 사용하여 재선언(re-declare)이 가능하며, var 변수를 업데이트할 수 있음
- 코드량이 많아진다면 어디에서 어떻게 사용될지 파악하기 힘들고 값이 바뀔 우려가 있음 👉 단점 보완을 위해 ```let```,```const```가 추가됨

```javascript
var a = 10 
// User can re-declare variable using var

var a = 8
// User can update var variable

a = 7
// Output = 7
```

### 2. ```let```
- Scope : Only block scoped (It can't be accessible outside the particular block)
- ```let```을 이용하여 재선언은 할 수 없으나, 변수를 업데이트할 수는 있음
- Users cannot re-declare the variable defined with the ```let``` keyword but can update it.

```javascript
let a = 10
let a = 8 // not allowed
a = 8 // allowed
console.log(a) // 8
```
```javascript
let a = 10
  if(true) {
    let a = 9
    console.log(a) // It prints 9
  }
console.log(a) // It prints 10
```

### 3. ```const```
- ```let```과 비슷하지만, 변수를 재선언하거나 업데이트할 수 없음
- Scope : Only block scoped
- property는 바꿀 수 없지만, value는 바꿀 수 있음

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
```javascript
const a = {
        prop1: 10,
        prop2: 9
    }
     
    a.prop1 = 3 // allowed
 
    a = {
        b: 10,
        prop2: 9
    } //not allowed
```

### 4. Hoisting
- ```var```선언문이나 ```function```선언문 등을 해당 scope의 선두로 옮긴 것처럼 동작하는 특성
- JS는 ```let```,```const```를 포함하여 모든 선언을 호이스팅함
- ```var```로 선언된 변수와는 달리, ```let```으로 선언된 변수를 선언문 이전에 참조하면 참조에러(ReferenceError) 발생

```javascript
console.log(a); // undefined
var a;

console.log(b); // Error: Uncaught ReferenceError: b is not defined
let b;
```

### 5. 결론
- 변수 선언에는 기본적으로 ```const```를 사용하고, 재할당이 필요한 경우에 한정해 ```let```을 사용


#### 참고사이트
Link 1 : https://www.geeksforgeeks.org/difference-between-var-let-and-const-keywords-in-javascript/
Link 2 : https://velog.io/@bathingape/JavaScript-var-let-const-%EC%B0%A8%EC%9D%B4%EC%A0%90
Link 3 : https://gist.github.com/LeoHeo/7c2a2a6dbcf80becaaa1e61e90091e5d
