# setInterval, setTimeout
- 일정 시간이 지난 후에 원하는 함수를 예약 실행(호출)할 수 있게 하는 것을 '호출 스케줄링(scheduling a call)'이라고 함<br>
- 호출 스케줄링을 구현하는 방법 : ```setTimeout```, ```setInterval``` 두 가지를 이용하는 방법
    - ```setTimeout``` : 일정 시간이 지난 후에 함수를 실행하는 방법
    - ```setInterval```: 일정 시간 간격을 두고 함수를 실행하는 방법
## 1. ```setInterval```
### 1) 구문
```javascript
let timerId = setInterval(func|code, [delay], [arg1], [arg2], ...)
```
- ```func|code``` : 실행하고자 하는 코드(함수)
- ```delay``` : 실행 전 대기 시간, 단위는 밀리초
- ```arg1```,```arg2```... : 함수에 전달할 인수들
👉 ```setTimeout```이 함수를 단 한 번만 실행하는 것과 달리 ```setInterval```은 함수를 주기적으로 실행하게 만듦
### 2) 예제
```javascript
// 2초 간격으로 메시지를 보여줌
let timerId = setInterval(() => alert('째깍'), 2000);

// 5초 후에 정지
setTimeout(() => { clearInterval(timerId); alert('정지'); }, 5000);
```
- 함수 호출을 중단하려면 ```clearInterval(timerId)```을 사용
- 위 예시를 실행하면 메시지가 2초 간격으로 보이다가 5초 이후에는 더 이상 메시지가 보이지 않음
- ```alert```창이 떠 있더라도 타이머는 멈추지 않음
3) 중첩 ```setTimeout```
- 무언가를 일정 간격을 두고 실행하는 방법 : ```setInterval``` 사용, ```setTimeout``` 사용 👉 ```setTimeout```을 이용하는 방법은 ```setInterval```을 사용하는 방법보다 유연함(호출 결과에 따라 다음 호출을 원하는 방식으로 조정해 스케줄링 할 수 있기 때문)
- CPU 소모가 많은 작업을 주기적으로 실행하는 경우에도 ````setTimeout```을 재귀 실행하는 방법이 유용함
- 중첩 ```setTimeout```을 이용하는 방법은 지연 간격을 보장하지만 ```setInterval```은 이를 보장하지 않음
```javascript
/** setInterval을 이용하지 않고 아래와 같이 중첩 setTimeout을 사용함
let timerId = setInterval(() => alert('째깍'), 2000);
*/

let timerId = setTimeout(function tick() {
  alert('째깍');
  timerId = setTimeout(tick, 2000); // (*)
}, 2000);
```
- 다섯 번째 줄 ```setTimeout```은 ```(*)```로 표시한 줄의 실행이 종료되면 다음 호출을 스케줄링함
## 2. ```setTimeout```
### 1) 구문
```javascript
let timeoutID = setTimeout(function[, delay, arg1, arg2, ...]);
let timeoutID = setTimeout(function[, delay]);
```
- ```function``` : 타이머가 만료된 뒤 실행할 함수
- ```delay``` : 주어진 함수 또는 코드를 실행하기 전에 기다릴 밀리초 단위 시간(생략 or 0을 지정할 경우 즉시- 다음 이벤트 사이클에 실행)
### 2) 예제
```javascript
function sayHi() {
  alert('안녕하세요.'); 
}

setTimeout(sayHi, 1000); // 안녕하세요.
```
```javascript
function sayHi(who, phrase) {
  alert( who + ' 님, ' + phrase );
}

setTimeout(sayHi, 1000, "바보", "안녕하세요."); // 바보 님, 안녕하세요.
```
### 3) ```clearTimeout```
```javascript
clearTimeout([식별자]);
```
- Node.js에서 ```setTimeout```을 호출하면 타이머 식별자(timer identifier)가 반환됨
- ```setTimeout```을 취소하고 싶을 때 이 반환된 식별자를 사용
```javascript
function timer(){
   console.log('3초뒤에 호출 될 코드입니다!!!');
}

var timerVar = setTimeout( timer, 3000);

clearTimeout(timerVar);
```


## 참고
- https://ko.javascript.info/settimeout-setinterval
- https://jin2rang.tistory.com/entry/setTimeout-clearTimeout
