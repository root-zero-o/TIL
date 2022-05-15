# 변수 쉐도잉(Shadowing)
## 1. 변수 쉐도잉이란?
- 변수 쉐도잉은 inner scope의 변수가 outer scope의 변수와 같은 이름을 가지고 선언되면 발생함
- 두 가지의 효과를 가진 protection mechanism의 한 종류라고 보면 됨
    - inner scope가 outer scope에서 선언된 변수에 접근하는 것을 막음
    - inner scope가 outer scope에서 선언된 변수를 변형시키는 것을 막음
- 쉐도잉은 의도하지 않은 결과를 불러올 수 있기 때문에 피해야 한다! 따라서 모호하지 않은 이름을 사용할 것

## 2. 예제
```javascript
let number = 10;

function displayDouble(){
  let number = 3;
  number *= 2;
  console.log(number); // 6
}

displayDouble();
console.log(number); // 10
```
- inner scope와 outer scope에서 ```number```라는 같은 이름의 변수를 선언함
- outer scope에서 선언된 변수 ```number```은 inner scope에서 선언된 변수 ```number```에 의해 쉐도잉됨 
- 다시 outer scope로 빠져나오면 outer scope에서 선언된 변수 ```number```로 적용됨

## 3. 실습문제
#### 문제
```javascript
function printTimesTable(a){
    for( i = 1 ; i <= 9 ; i++ ){
        console.log( a + " * " + i + " = " + a*i );
    }
}

for( var i = 2 ; i <= 9 ; i++ ){
    printTimesTable(i);
}
```
이대로 실행하면 2단만 실행됨 👉 9단까지 정상적으로 실행되도록 shadowing 효과를 추가해보기

#### 풀이
```javascript
function printTimesTable(a){
    for( let i = 1 ; i <= 9 ; i++ ){
        console.log( a + " * " + i + " = " + a*i );
    }
}

for( var i = 2 ; i <= 9 ; i++ ){
    printTimesTable(i);
}
```
- 기존 문제에서는 변수 i값을 function 안에서 i = 1로 업데이트를 해주었기 때문에, function printTimesTable(2)가 실행된 후, i 값이 10으로 업데이트되어 밖으로 나오게되고, 따라서 i는 9보다 커지므로 더이상 함수는 실행되지 않음
- function안에 let을 추가하여 inner scope에서 변수를 새롭게 선언한 것처럼 만들어, inner scope에서 i가 1 ~ 9까지 반복하고, 함수를 빠져나와도 outer scope의 변수에 영향을 미치지 않아 9단까지 정상적으로 실행됨

## 참고
- https://mayuminishimoto.medium.com/understanding-variable-shadowing-with-javascript-58fc108c8f03
- [프로그래머스 실습 문제](https://programmers.co.kr/learn/courses/3/lessons/211)
