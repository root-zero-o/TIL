# reduce()
## 1. ```reduce()```란?
```javascript
배열.reduce((누적값, 현잿값, 인덱스, 요소) => {return 결과 }, 초깃값);
```
```reduce()```는 빈 요소를 제외하고 배열 내에 존재하는 각 요소에 대해 ```callback```함수를 한 번식 실행
-  ```callback``` : 배열의 각 요소에 대해 실행할 함수
    - ```누적값``` : 콜백함수의 반환값 누적
    - ```현잿값``` : 처리할 현재 요소
    - ```인덱스```: 처리할 현재 요소의 인덱스 (Optional)
## 2. 예제
```javascript
const oneTwoThree = [1, 2, 3];
result = oneTwoThree.reduce((acc, cur, i) => {
  console.log(acc, cur, i);
  return acc + cur;
}, 0);
// 0 1 0
// 1 2 1
// 3 3 2
result; // 6
```
- 초깃값을 적어주지 않으면 자동으로 초깃값이 0번째 인덱스의 값이 됨

## 3. ```reduceRight()```
- ```reduce```와 동작은 같지만 요소 순회를 오른쪽에서부터 왼쪽으로 함
```javascript
result = oneTwoThree.reduceRight((acc, cur, i) => {
  console.log(acc, cur, i);
  return acc + cur;
}, 0);
// 0 3 2
// 3 2 1
// 5 1 0
result; // 6
```

## 참고
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce
- https://www.zerocho.com/category/JavaScript/post/5acafb05f24445001b8d796d
