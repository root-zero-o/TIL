# 이터레이션 프로토콜(Iteration protocol)
- 데이터 컬렉션을 순회하기 위한 프로토콜(미리 약속된 규칙)
- 이터레이션 프로토콜을 준수한 객체는 ```for...of```문으로 순회할 수 있고 Spread 문법의 피연산자가 될 수 있음
- 이터레이션 프로토콜에는 이터러블 프로토콜(iterable protocol)과 이터레이터 프로토콜(iterator protocol)이 있음
## 1. 이터러블(iterable)
- 이터러블 프로토콜을 준수한 객체를 '이터러블'이라 함
- ```Symbol.iterator```메소드를 구현하거나 프로토타입 체인에 의해 상속한 객체
- ```Symbol.iterator```메소드는 이터레이터를 반환함
- String, Array, TypedArray, Map, Set 등은 내장되어 있는 이터러블 객체
```javascript
const array = [1, 2, 3];

// 배열은 Symbol.iterator 메소드를 소유한다.
// 따라서 배열은 이터러블 프로토콜을 준수한 이터러블이다.
console.log(Symbol.iterator in array); // true

// 이터러블 프로토콜을 준수한 배열은 for...of 문에서 순회 가능하다.
for (const item of array) {
  console.log(item);
}
```
- 일반 객체는 이터레이션 프로토콜을 준수(```Symbol.iterator```메소드를 소유)하지 않기 때문에 이터러블이 아님
- 따라서 일반 객체는 ```for...of```문에서 순회할 수 없고, ```Spread```문법의 대상으로 사용할 수 없음
- 일반 객체의 경우에도 이터러블 프로토콜을 따르도록만 하면 이터러블이 됨

## 2. 이터레이터(iterator)
- ```next```메소드를 소유하며, ```next```메소드를 호출하면 이터러블을 순회하며 ```value```,```done``` 프로퍼티를 갖는 이터레이터 리절트 객체를 반환함
- 이터레이터 프로토콜을 준수한 객체가 이터레이터

- 추후 추가 정리
## 참고
- https://equal-blog.tistory.com/entry/%EC%9D%B4%ED%84%B0%EB%A0%88%EC%9D%B4%EC%85%98-%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9CIteration-Protocol
- https://poiemaweb.com/es6-iteration-for-of
