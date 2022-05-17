# 프로토타입(prototype)
## 1. 개념
- 자바스크립트는 객체를 상속하기 위해 프로토타입(prototype)이라는 방식을 사용함(프로토타입 기반 언어)
- 모든 객체들은 메소드와 속성들을 상속 받기 위한 템플릿으로써 *프로토타입 객체(protorype object)* 를 가진다는 의미
- ☝️프로토타입 체인(prototype chain) : 프로토타입 객체도 또 다시 상위 프로토타입 객체로부터 메소드와 속성을 상속받을 수 있음 
- 상속되는 속성과 메소드들은 각 객체가 아니라 객체의 생성자의 ```prototype```이라는 속성에 정의되어 있는 것
- 객체는 자신을 생성한 생성자의 ```prototype```에 대한 참조인 ```__proto__```와 ```constructor``` 속성을 자동으로 가짐

## 2. 예제
```javascript
function Person(first, last, age, gender, interests) {
  // 속성과 메소드 정의
  this.first = first;
  this.last = last;
}

var person1 = new Person('Bob', 'Smith', 32, 'male', ['music', 'skiing']);
```
![MDN-Graphics-person-person-object-2](https://user-images.githubusercontent.com/97326130/168729427-69fa19b0-50f7-4170-a86f-4b3f46726edd.png)<br>
- 이때, ```object```에 정의되어 있는 메소드를 ```person1```에서 아래와 호출하면
```javascript
person1.valueOf()
```
1) 브라우저는 우선 ```person1``` 객체가 ```valueOf``` 메소드를 가지고 있는지 체크 > 없음
2) ```person1```의 프로토타입 객체(```Person()``` 생성자의 프로토타입)에 ```valueOf()```메소드가 있는지 체크 > 없음
3) ```Person()``` 생성자의 프로토타입 객체의 프로토타입 객체(```Object()``` 생성자의 프로토타입)가 ```valueOf``` 메소드를 가지고 있는지 체크 > 있음 > 호출
<br>⛔ 프로토타입 체인에서 한 객체의 메소드와 속성들이 다른 객체로 복사되는 것이 아님 !! 체인을 타고 올라가며 접근할 뿐 !!

## 3. 특정 객체의 프로토타입 객체에 접근하는 방법
- ```__proto__``` 속성을 통해 특정 객체의 프로토타입 객체에 접근 가능
```javascript
person1.__proto__
person1.__proto__.__proto__
```
- ```Object.getPrototypeOf(obj)``` 함수를 통해 객체의 프로토타입 객체에 바로 접근할 수 있음!

## 참고
- https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Object_prototypes
