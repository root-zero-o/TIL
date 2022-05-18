# map()
## 1. ```map()```이란?
- 주어진 배열의 값들을 오름차순으로 접근해 callback함수를 통해 새로운 값을 정의하고 신규 배열을 만들어 반환
- callback 함수를 *각각의 요소에 대해 한번씩* 순서대로 불러 그 함수의 반환값으로 새로운 배열을 만듦
- callback 함수는 배열 값이 들어있는 인덱스에 대해서만 호출됨(값이 삭제되거나 아직 값이 할당/정의되지 않은 인덱스에 대해서는 호출X)
#### 예제
```javascript
const numbers = [1, 2, 3, 4, 5]; 
const result = numbers.map(number => number * number); 

console.log(numbers); // [1, 2, 3, 4, 5]; 
console.log(result); // [1, 4, 9, 16, 25]
```
## 2. 사용법
- callback 함수를 통해 주어진 3개의 인자(요소 값, index, 순회하는 대상 객체)를 사용해 새로운 값을 만드는 함수를 등록
```javascript
const numbers = [1]; 
numbers.map((number, index, source) => { 
  // number: 요소값 
  // index: source에서 요소의 index 
  // source: 순회하는 대상 
  console.log(number); // 1 
  console.log(index); // 0 
  console.log(source); // [1] 
  
  return number * number; 
});
```
- ```map```을 통해 새로운 형태의 값을 정의할 수 있음
```javascript
// 프로그래밍 이름 길이 구하기 
const programingLanguages = ["javascript", "java", "c#", "c++", "c"]; 
const lengthOfProgramingLanguages = programingLanguages.map(language => language.length); 
console.log(lengthOfProgramingLanguages); // [10, 4, 2, 3, 1];
```
## 3. 주의사항
- ```map```은 객체를 직접 사용하거나 변형시키지 않지만 callback함수를 통해 수정할 수 있음
- ```callback```함수가 호출되는 범위는 ```callback```함수가 처음 호출되기 이전이고, ```map```이 순회하는 도중에 추가된 요소는 접근X
- 순회하는 도중 수정이 일어나면 변경된 값이 ```callback```에 전달되고 삭제된 요소는 접근X
```javascript
// array 요소가 추가되는 경우 
const numbers = [1, 2, 3, 4, 5]; 

const result = numbers.map(number => { 
  numbers.push(number); 
  return number * number; 
}); 

console.log(result); // [1, 4, 9, 16, 25];
```
```javascript
// array 요소가 수정되는 경우 
const numbers = [1, 2, 3, 4, 5]; 

const result = numbers.map(number => { 
  numbers.pop(); 
  return number * number; 
}); 

console.log(result); // [1, 4, 9, empty × 2];
```
## 4. 활용법
### 1) 고차 함수 사용하기
- 미리 정해둔 식이나 정의되어 있는 식을 이용할 수 있음
```javascript
const numbers = [1, 2, 3, 4, 5];

//제곱근 구하기
const squares = numbers.map(Math.sqrt);

console.log(squares);
// [1, 1.4142135623730951, 1.7320508075688772, 2, 2.23606797749979]

//곱 구하기
const double = value => value * 2;
const doubles = numbers.map(double);

console.log(doubles); 
// [2, 4, 6, 8, 10]
```
### 2) 새로운 형태의 값 생성하기
```javascript
const users = [ 
  { name: 'YD', age: 22 }, 
  { name: 'Bill', age: 32 }, 
  { name: 'Andy', age: 21 }, 
  { name: 'Roky', age: 35 },
];

const ages = users.map(user => user.age); 

console.log(ages); 
// [22, 32, 21, 35]
```
### 3) 특정 요소만 재정의하기
```javascript
const users = [ 
  { name: 'YD', age: 22 }, 
  { name: 'Bill', age: 32 }, 
  { name: 'Andy', age: 21 }, 
  { name: 'Roky', age: 35 }, 
]; 

const newUsers = users.map(user => { 
  if (user.name === 'YD') { 
    return { ...user, age: 18 }; 
   } 
   
   return { ...user }; 
}); 

console.log(newUsers); 
// [{name: "YD", age: 18}, {name: "Bill", age: 32}, {name: "Andy", age: 21}, {name: "Roky", age: 35}]
```
### 4) 문자를 배열로 바꾸기
```call```을 이용하면 다른 객체의 context를 사용해 문자를 배열로 반환하는 데에 사용함
```javascript
const message = 'Hello world'; 

const newMessage = Array.prototype.map.call(message, char => `${char}`); 

console.log(newMessage); 
// ["H", "e", "l", "l", "o", " ", "w", "o", "r", "l", "d"]
```
## 참고
- https://7942yongdae.tistory.com/entry/Javascript-Array-map-%EC%82%AC%EC%9A%A9%EB%B2%95
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map
