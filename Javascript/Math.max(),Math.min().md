# Math.max(), Math.min()

- ```Math.max()``` : 입력 값으로 받은 0개 이상의 숫자 중 가장 큰 숫자를 반환함
- ```Math.min()``` : 입력 값으로 받은 0개 이상의 숫자 중 가장 작은 숫자를 반환함

```javascript
console.log(Math.max(1, 3, 2)); // 3
console.log(Math.max(-1, -3, -2)); // -1

const array1 = [1, 3, 2];
console.log(Math.max(...array1)); // 3
```
```javascript
var x = 10, y = -20;
var z = Math.min(x, y);
console.log(z); // -20
```
## 참고
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Math/min
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Math/max
