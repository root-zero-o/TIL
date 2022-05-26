# 단축 평가(short-circuit evaluation) 논리 계산법
## 1. ```&&```연산자로 코드 단축
``` A && B ``` 연산자 : A가 true이면 B가 결과값, A가 false이면 A가 결과값
```javascript
console.log(true && 'hello'); // hello
console.log(false && 'hello'); // false
console.log('hello' && 'bye'); // bye
console.log(null && 'hello'); // null
console.log(undefined && 'hello'); // undefined
console.log('' && 'hello'); // ''
console.log(0 && 'hello'); // 0
console.log(1 && 'hello'); // hello
console.log(1 && 1); // 1
```

## 2. ```||```연산자로 코드 단축
```A || B ``` : A가 true일 경우 결과는 A, A가 false일 경우 결과는 B
```javascript
const namelessDog = {
  name: ''
};

function getName(animal) {
  const name = animal && animal.name;
  if (!name) {
    return '이름이 없는 동물입니다';
  }
  return name;
}

const name = getName(namelessDog);
console.log(name); // 이름이 없는 동물입니다.
```
```javascript
const namelessDog = {
  name: ''
};

function getName(animal) {
  const name = animal && animal.name;
  return name || '이름이 없는 동물입니다.';
}

const name = getName(namelessDog);
console.log(name); // 이름이 없는 동물입니다.
```
위 아래 코드는 같다 !

## 참고 
- [벨로퍼트와 함께하는 모던 자바스크립트 - 2장 03. 단축 평가 논리 계산법](https://learnjs.vlpt.us/useful/03-short-circuiting.html)
