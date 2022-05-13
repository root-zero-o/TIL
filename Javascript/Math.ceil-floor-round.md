# 올림, 내림, 반올림

## 1. ```Math.ceil()``` : 올림
- 입력받은 숫자보다 크거나 같은 정수 중 가장 작은 정수를 리턴함
```javascript
console.log(Math.ceil(1)); // 1
console.log(Math.ceil(1.2222)); // 2

console.log(Math.ceil(null)); // 0
console.log(Math.ceil(0)); // 0

console.log(Math.ceil(-1)); // -1
console.log(Math.ceil(-1.777)); // -1
```
- 자릿수 지정
```javascript
console.log(Math.ceil(1.222 * 10)); // 1.3
console.log(Math.ceil(1.222 * 100)); // 1.23

console.log(Math.ceil(1222 / 10)); // 1230
console.log(Math.ceil(1222 / 100)); // 1300
```

## 2. ```Math.floor()``` : 내림
- 입력받은 숫자보다 작거나 같은 정수 중 가장 큰 정수를 리턴함
```javascript
console.log(Math.floor(1)); // 1
console.log(Math.floor(1.2222)); // 1

console.log(Math.floor(null)); // 0
console.log(Math.floor(0)); // 0

console.log(Math.floor(-1)); // -1
console.log(Math.floor(-1.777)); // -2
```
- 자릿수 지정
```javascript
console.log(Math.floor(1.222 * 10)); // 1.2
console.log(Math.floor(1.222 * 100)); // 1.22

console.log(Math.floor(1222 / 10)); // 1220
console.log(Math.floor(1222 / 100)); // 1200
```

## 3. ```Math.round()``` : 반올림
- 파라미터로 입력받은 숫자의 소수점 이하의 값이 0.5보다 크면 올림, 0.5보다 작으면 내림, 같으면 입력받은 수보다 큰 다음 정수를 리턴
```javascript
console.log(Math.round(1)); // 1
console.log(Math.round(1.2222)); // 1
console.log(Math.round(1.5555)); // 2

console.log(Math.round(null)); // 0
console.log(Math.round(0)); // 0

console.log(Math.round(-1.111)); // -1
console.log(Math.round(-1.777)); // -2
```
- 자릿수 지정
```javascript
console.log(Math.round(1.222 * 10)); // 1.2
console.log(Math.round(1.5 * 10)); // 1.5
console.log(Math.round(1.7777 * 10)); // 1.8

console.log(Math.round(1001 * 10)); // 1000
console.log(Math.round(1005 * 10)); // 1010
console.log(Math.round(1007 * 10)); // 1010
```

## 참고
- https://hianna.tistory.com/446
