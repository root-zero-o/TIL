# 함수선언식 vs 함수표현식
## 함수선언식(Function declaration)
```function 함수명(){ 구현 로직 }```
```javascript
function name(param1, param2){
  body...return;
}
```
- 하나의 함수는 한 가지 일만 함
- 함수 이름 : doSomething, command, verb 형태로 이름 지정
- JS에서 ```function```은 object로 간주함
- parameter의 type 모호 👉 Typescript에서는 명시하도록 되어 있음 !

## 함수표현식(Function expression)
```const 함수명 = function(){ 구현로직 }```
유연한 자바스크립트 언어의 특징을 활용한 선언방식
```javascript
print();
const print = function () { //anonymous function
    console.log('print');
};
print ();
const printAgain  = print;
printAgain();    
```
- 함수를 ```print```에 할당 👉 함수를 호출하듯이 ```print()```라고 호출하면 'print'가 출력됨
- ```printAgain```에 다시 할당 👉 ```printAgain()```으로 호출하면 'print'가 출력됨

## 함수선언식과 함수표현식의 차이점
- 함수선언식 : 함수가 할당되기 전에도 호출이 가능함(Hoisting에 영향 받음)
- 함수표현식 : 함수가 할당된 다음 호출이 가능함(Hoisting에 영향 받지 않음 👉 클로져, 콜백으로 사용 가능)

## 참고
- https://joshua1988.github.io/web-development/javascript/function-expressions-vs-declarations/
- https://www.youtube.com/watch?v=e_lU39U-5bQ&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=5

