# This
## 1. 개념
- ```this```는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수(self-reference variable)
- ```this```를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메소드를 참조할 수 있음
- 즉! ```this```는 "호출한 놈"

## 2. 상황별 this

### 1) 단독으로 쓴 ```this```
- 전역 실행 맥락에서 ```this```는 엄격 모드 여부에 관계 없이 전역 객체를 참조
- ```globalThis```프로퍼티를 사용해 코드가 실행중인 현재 컨텍스트와 관계없이 항상 전역객체를 얻을 수 있음
```javascript
// 웹 브라우저에서는 window 객체가 전역 객체
console.log(this === window); // true

a = 37;
console.log(window.a); // 37

this.b = "MDN";
console.log(window.b)  // "MDN"
console.log(b)         // "MDN"
```
### 2) 함수 안에서 쓴 ```this```
함수 내부에서 ```this```값은 함수를 호출한 방법에 의해 좌우됨
```javascript
function f1() {
  return this;
}

f1() === window; // true
```
- 엄격모드가 아니고, ```this```의 값이 호출에 의해 설정되지 않으므로, ```window```인 전역 객체를 참조함(함수의 주인인 window에게 바인딩됨)
```javascript
"use strict";
 
function myFunction() {
  return this;
}
console.log(myFunction()); //undefined
```
- 엄격모드에서 ```this```값은 실행 문맥에 진입하며 설정되는 값을 유지하기 때문에, ```this```는 ```undefined```로 남아있음
- ```f2```를 객체의 매서드나 속성(```window.f2()```)으로써가 아닌 직접 호출했기 때문에 ```this```는 ```undefined```

### 3) 메서드 안에서 쓴 ```this```
메서드 호출 시 메서드 내부 코드에서 사용된 ```this```는 해당 메서드를 호출한 객체로 바인딩됨
```javascript
var person = {
  firstName: 'John',
  lastName: 'Doe',
  fullName: function () {
    return this.firstName + ' ' + this.lastName;
  },
};
person.fullName(); //"John Doe"
```

### 4) 이벤트 핸들러 안에서 쓴 ```this```
이벤트 핸들러에서 this는 이벤트를 받는 HTML 요소를 가리킴
```javascript
var btn = document.querySelector('#btn')
btn.addEventListener('click', function () {
  console.log(this); //#btn
});
```

### 5) 생성자 안에서 쓴 ```this```
- 생성자 함수가 생성하는 객체로 ```this```가 바인딩됨
- new 키워드를 빼먹으면 일반 함수 호출과 같아져 ```this```가 ```window```에 바인딩됨
```javascript
function Person(name) {
  this.name = name;
}
 
var kim = new Person('kim');
var lee = new Person('lee');
 
console.log(kim.name); //kim
console.log(lee.name); //lee
```

### 6) 명시적 바인딩을 한 ```this```
- 명시적 바인딩 : 짝을 지어주는 것(이 this는 내꺼야)
- ```apply()```와 ```call()```메서드는 인자를 ```this```로 만들어주는 기능을 함
```javascript
function whoisThis() {
  console.log(this);
}
 
whoisThis(); //window
 
var obj = {
  x: 123,
};
 
whoisThis.call(obj); //{x:123}
```
### 7) 화살표 함수로 쓴 this
- 전역 맥락에서 실행되더라도 ```this```를 새로 정의하지 않고, 바로 바깥 함수나 클래스의 ```this```를 씀
```javascript
var Person = function (name, age) {
  this.name = name;
  this.age = age;
  this.say = function () {
    console.log(this); // Person {name: "Nana", age: 28}
 
    setTimeout(function () {
      console.log(this); // Window
      console.log(this.name + ' is ' + this.age + ' years old');
    }, 100);
  };
};
var me = new Person('Nana', 28);
 
me.say(); //global is undefined years old
```
- 내부 함수에서 ```this```가 전역 객체를 가리키는 바람에 다른 결과가 나옴
```javascript
var Person = function (name, age) {
  this.name = name;
  this.age = age;
  this.say = function () {
    console.log(this); // Person {name: "Nana", age: 28}
 
    setTimeout(() => {
      console.log(this); // Person {name: "Nana", age: 28}
      console.log(this.name + ' is ' + this.age + ' years old'); 
    }, 100);
  };
};
var me = new Person('Nana', 28); //Nana is 28 years old
```
- 화살표 함수로 바꾸면 제대로 된 결과가 나옴
- 생성자 공부한 뒤 다시 정리할 것

## 참고
- https://nykim.work/71
