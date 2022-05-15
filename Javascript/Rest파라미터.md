# Rest 파라미터

## 1. Rest 파라미터란?
```function f(a, b, ...theArgs){  }```

- ```...(Spread 연산자)```를 사용하여 함수의 파라미터를 작성한 형태
- Rest파라미터를 사용하면 함수의 파라미터로 오는 값들을 배열로 전달받을 수 있음
- 사용방법 : 파라미터 앞에 ```...```를 붙인다 !

```javascript
function test(a, b, ...theArgs){
    console.log(a, b); //1, 2
    console.log(theArgs); // [3, 4, 5]
}
test(1, 2, 3, 4, 5);
```

## 2. 주의할 점⛔
- 처음이나 중간에 올 수 없고, 마지막에만 올 수 있음
- 함수 정의에는 하나의 ```...```만 존재할 수 있음

## Rest parameter vs ```arguments```객체
- ```arguments``` 객체는 실제 배열이 아님. rest파라미터는 배열이므로 ```sort```,```map```,```forEach```,```pop```등의 method를 직접 적용할 수 있음
- arrow function에 ```arguments```는 사용할 수 없으며, rest 파라미터는 더 유연한 코드를 작성할 수 있음 👉 rest파라미터 사용 권장

## 참고
- https://chanhuiseok.github.io/posts/js-9/
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/rest_parameters
- https://jeong-pro.tistory.com/117
