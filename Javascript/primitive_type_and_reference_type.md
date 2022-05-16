 # 원시 타입(Primitive type) vs 참조 타입(Reference type)

자바스크립트는 원시 타입(primitive type)과 참조 타입(reference type)이라는 두 가지 자료형을 제공함
- 원시 타입 : 숫자(Number), 불리언(Boolean), null, undefined, 문자열(string)
- 참조 타입 : 객체(Object), 배열(Array), 함수(function)

## 1. 원시 타입
### 1) 특징
- 변수에 할당될 때 메모리 상에 고정된 크기로 저장되고, 해당 변수가 원시 데이터의 값을 보관함
- 변수 선언, 초기화, 할당시 값이 저장된 메모리 영역에 직접적으로 접근
- 즉, 변수에 새 값이 할당될 때 변수에 할당된 메모리 블럭에 저장된 값을 바로 변경한다는 뜻(Access by value)
### 2) 변수 복사
각 변수 간에 원시 타입 데이터를 복사할 경우 데이터의 값이 복사됨
```javascript
var x = 100;
var y = x;
y; // 100
```
- 여기서 문자열(string)은 크기가 고정되어 있지 않지만 원시타입처럼 동작함
```javascript
var x = "Hello";
var y = x;
x = "Hi";
x; // Hi
y; // Hello
```

## 2. 참조 타입
### 1) 특징
- 크기가 정해져 있지 않음
- 변수에 할당될 때 값이 직접 해당 변수에 저장될 수 없고, 변수에는 데이터에 대한 참조만 저장됨
- 변수의 값이 저장된 힙(heap) 메모리의 주소값을 저장함
- 변수의 값이 저장된 메모리 블럭의 주소를 가지고 있고, 자바스크립트 엔진이 변수가 가지고 있는 메모리 주소를 이용해 변수의 값에 접근함(Access by reference)
### 2) 변수 복사
각 변수 간에 참조 타입 데이터를 복사할 경우 데이터의 참조가 복사됨
```javascript
var x = {count : 100}; // 참조 타입 선언
var y = x;
x.count = 99;
y.count; // 99
```
- x와 y는 동일한 참조를 담고 있으며, 따라서 동일한 객체를 가리킴
### 3) 예제
```javascript
var list1 = [1, 2, 3];	// 메모리 주소 : 8765e 라고 가정
var list2 = [1, 2, 3];	// 메모리 주소 : 9524d 라고 가정

var isSame = list1 === list2;	8765e === 9524d

console.log(isSame);	// false
```
- ```list1```,```list2```안의 요소는 같지만 배열을 새롭게 만들어 변수에 담고 있음
- 각자 새로운 메모리 위치를 만들어 저장하고 그 위치를 참조하여 변수에 해당 위치 값을 저장하는 것과 같음
- 따라서 결과는 ```false```
```javascript
var list3 = [ 1, 2, 3];
var list4 = list3;

var isSame = list3 === list4;

console.log(isSame);	// true
```
- 새롭게 배열을 생성하지 않고 ```list3```의 위치값을 그대로 ```list4```에 넣는 것이기 때문에 위치 값이 같음
- 따라서 결과는 ```true```
```javascript
let foo = 5; // 원시 값

function addTwo(num) {
   num += 2;
}

function addTwo_v2(foo) {
   foo += 2;
}

addTwo(foo);
console.log(foo);   // 5

addTwo_v2(foo);
console.log(foo);   // 5
```
- 함수의 구문들을 실행하기 전에 자바스크립트는 원래 전달된 인수(원시값)를 복사해 로컬 복사본을 생성함
- 이 복사본은 함수의 스코프 내에서만 존재하며, 함수 정의 내에 지정한 식별자를 통해 접근 가능함
- 함수 구문 실행 후에도 로컬 인수는 외부 변수 ```foo```에 어떤 방법으로든 접근할 수 없음!
- 결과적으로, 함수들 내부의 모든 변경의 그 복사본으로 작업하였기 때문에, 원본 ```foo```에 전혀 영향을 주지 않음

## 참고
- https://weicomes.tistory.com/133
- https://velog.io/@surim014/JavaScript-Primitive-Type-vs-Reference-Type
- 
