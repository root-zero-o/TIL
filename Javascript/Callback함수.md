# 콜백함수(Callback function)

## 1. 콜백함수란?
- 다른 함수에 매개변수로 넘겨준 함수를 말함(인자로 넘겨지는 함수)
- 매개변수로 넘겨받은 함수는 일단 넘겨받고, 때가 되면 나중에 호출(called back)한다는 개념
```javascript
function mainFunc(param1, param2, callbackFunc){
  callbackFunc(result)
}
```
## 2. 예제
```javascript
function returnName(callback){
  callback("babo");
  console.log("만나서 반갑습니다");
}

function sayHello(name){
  console.log("안녕하세요 "+name+ "씨");
}

returnName(sayHello) 
// 안녕하세요 babo씨
// 만나서 반갑습니다
```
- returnName : 파라미터에 callback이라는 함수가 선언되어 있음
- returnName함수의 파라미터로 받게되는 함수(sayHello)는 "babo"이라는 string을 인자로 받음
- returnName 함수는 sayHello라는 함수를 파라미터로 가지고 호출됨
- returnName 함수는 sayHello 함수를 인자로 받아야하므로 sayHello 함수가 ```먼저``` 실행된 뒤 returnName 함수가 실행됨

## 참고
- https://bigtop.tistory.com/35
- https://jason9319.tistory.com/406
