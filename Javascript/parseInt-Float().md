# ```parseInt()```,```parseFloat()```함수로 문자열을 수로 바꾸기

## 1. ```parseFloat()```함수
```javascript
parseFloat(string)
```
- 수로 시작할 때 그 수를 실수로 바꿈
- 띄어쓰기로 여러 개의 수가 있으면 첫 번째 수만 바꿈
- 공백으로 시작하면 공백 무시, 수가 아닌 문자로 시작하면 ```NaN``` 반환
- 소수점이 두 개 이상 존재할 경우 두 번째 소수점 무시
- ```+```,```-```, 숫자, 소수점, 지수 외의 다른 글자를 발견할 경우 해당 문자 이전까지의 문자만 사용해 파싱
```javascript
console.log(parseFloat('3.14')); // 3.14
console.log(parseFloat('    3.14     ')); // 3.14
console.log(parseFloat('3.14어쩌고저쩌고')); // 3.14

console.log(parseFloat('FF2')); // NaN
```
## 2.```parseInt()```함수
```javascript
parseInt(string, n) 
```
string을 n진법일 때의 값으로 바꿈(n은 옵션, 입력하지 않으면 10으로 처리)
- 문자열 인자를 파싱하여 특정 진수(수의 진법 체계에서 기준이 되는 값)의 정수를 반환함(소수 부분은 버림)
- 공백이 아닌 첫 문자를 숫자로 변환할 수 없는 경우, ```NaN```을 반환함

*파싱(parsing) :  어떤 페이지(문서,html등)에서 내가 원하는 데이터를 특정 패턴이나 순서로 추출해 가공하는 것*
*파싱을 수행하는 프로그램은 파서(parser)라고 부름*

## 참고
- [파싱이란?](https://www.scienceall.com/%ED%8C%8C%EC%8B%B1parsing/)
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/parseFloat
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/parseInt
