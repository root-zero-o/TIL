# Promise
## 1. Promise 객체란?
```javascript
let promise = new Promise(function(resolve, reject) {
  // executor 
});
```
- ```executor``` : 결과를 최종적으로 만들어내는 함수. 상황에 따라 인수로 넘겨준 콜백 중 하나를 반드시 호출해야 함
- ```resolve(value)``` : 일이 성공적으로 끝난 경우, 그 결과를 나타내는 ```value```와 함께 호출
- ```reject(error)``` : 에러 발생 시 에러 객체를 나타내는 ```error```와 함께 호출
- ```new Promise``` 생성자가 반환하는 ```promise``` 객체의 내부 프로퍼티
    - ```state``` : 처음엔 "pending"(보류)였다가 ```resolve```가 호출되면 "fulfilled", ```reject```가 호출되면 "rejected"로 변함
    - ```result```: 처음엔 undefined였다가 ```resolve(value)```가 호출되면 value로, ```reject(error)```가 호출되면 error로 변함

## 2. then, catch
- ```then``` : 해당 Promise가 성공했을 때의 동작을 지정함. Promise를 반환함
- ```catch```: 해당 Promise가 실패했을 때의 동작을 지정함. Promise를 반환함<br>
👉 연속적으로 호출 가능함. 즉, 체인 형태로 활용 가능하다!

## 3. 메서드 체이닝(method chaining)
- ```then```과 ```catch``` 메서드는 또 다른 promise 객체를 리턴함
- 리턴된 promise 객체는 인자로 넘김 콜백 함수의 리턴값을 다시 ```then```과 ```catch```메서드를 통해 접근 가능
```javascript
fetch('https://www.google.com')  
  .then((response) => response.text())
  .then((result) => { console.log(result); });
console.log('end!');
```
위 코드를 해석하면?
```javascript
fetch('https://www.google.com') 
// 1. 제일 처음 fetch 가 return 한 Promise obj.는 pending 상태 (작업 진행중)
// 2. 만약 네트워크가 끊겨서 response가 안되었다면 rejected 상태
    // 2-1. 만약 실패하게 된다면 실패 이유가 Promise 객체에 저장 (작업 실패 정보)
// 3. 이후에 response를 정상적으로  받으면 fulfilled 상태
    // 3-1. 만약 작업이 성공해서 fulfilled 상태가 되면, 객체는 그 작업의 성공 결과도 함께 저장
  .then((response) => response.text()) 
    // 3-2. 위의 response 가 작업에 대한 성공 결과 (작업 성공 결과)
  .then((result) => { console.log(result); }); 
```
```javascript
fetch('https://www.google.com')  // [ promise(fetch) : fulfilled ]
  .then((response) => response.text()) // [ promise(then) : pending ]
     // [ promise(call back) : fulfilled ]  =>  *[ promise(then) : pending => fulfilled, 작업성공결과 저장 ]
     // [ promise(call back) : rejected ]  =>  *[ promise(then) : pending => rejected, 작업 실패내용 저장 ]
```

## 참고
- https://elvanov.com/2597
- https://github.com/kordobby/amazon/blob/main/React/data_array/fetch_then().md
 
