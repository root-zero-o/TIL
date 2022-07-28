# 함수선언식 vs 함수표현식
## 함수선언식(Function declaration)
```function 함수명(){ 구현 로직 }```
```javascript
// 함수 선언문
let add = function add(x, y){
  return x + y;
}

// 함수 호출
console.log(add(2, 5));  // 7
```
- 함수 이름을 생략할 수 없다.
- 함수선언문은 표현식이 아닌 문으로, 변수에 할당할 수 없다.
- 하지만 JS 엔진은 코드의 문맥에 따라 다르게 해석하기 때문에, 변수에 할당되는 것처럼 동작한다.

```javascript
function foo() { console.log("foo") }
foo();  // "foo"
```
- 위의 예시에서 ```foo```는 ``함수 몸체 내에서만`` 참조할 수 있는 식별자이다.
- 하지만 ```foo```로 함수를 호출할 수 있는 이유는, ```foo```가 JS 엔진이 암묵적으로 생성한 식별자이기 때문이다.
- JS 엔진은 생성된 함수를 호출하기 위해 함수 이름과 ``동일한 이름의 식별자를 암묵적으로 생성``하고, 거기에 함수 객체를 할당한다.

## 함수표현식(Function expression)
```const 함수명 = function(){ 구현로직 }```

```javascript
let add = function foo (x, y) {
  return x + y;
}

// 함수 이름을 가리키는 식별자로 호출한다.
console.log(add(2, 5));  // 7
```

- 함수 표현식은 선언식과 다르게 '표현식인 문'이다. 따라서 변수에 할당이 가능하다.

## 함수선언식과 함수표현식의 차이점
- ```함수 호이스팅(function hoisting)``` : 함수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 JS 고유의 특징
- 차이점
    - 함수선언식 : 함수가 할당되기 전에도 호출이 가능함(Hoisting에 영향 받음)
    - 함수표현식 : 함수가 할당된 다음 호출이 가능함(Hoisting에 영향 받지 않음 👉 클로져, 콜백으로 사용 가능)

### 호이스팅이 선언식에서만 일어나는 이유🤔
- 함수의 생성시점이 다르기 때문이다.
    - 함수 선언식 : ```런타임 이전에``` JS 엔진에 의해 먼저 실행되어 함수 객체가 먼저 생성된다.
    - 함수 표현식 : 변수에 할당되는 값이 함수 리터럴이다. 즉, 변수 선언은 런타임 이전에 실행되나 변수 할당문은 런타임에 평가되므로, 함수 표현식의 함수 리터럴도 ```런타임에 평가```되어 함수 객체가 된다. 따라서 함수 표현식으로 함수를 정의하면 함수 호이스팅이 아닌 ```변수 호이스팅```이 발생한다. <br>
    
 **함수 호이스팅은 함수 호출 전, 반드시 함수를 선언해야 한다는 규칙을 무시하기 때문에 함수 표현식 사용이 권장된다.*

## 참고
- 모던 자바스크립트 Deep Dive (이웅모 저)
- https://joshua1988.github.io/web-development/javascript/function-expressions-vs-declarations/
- https://www.youtube.com/watch?v=e_lU39U-5bQ&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=5

