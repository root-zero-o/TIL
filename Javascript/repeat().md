# Repeat()
```javascript
str.repeat(count);
```
주어진 문자열을 ```count```만큼 반복하여 붙인 뒤, 새로운 문자열로 반환하면 함수
- 문자열을 반복한 값을 ```repeat()```함수로 반복문을 사용해 반환 가능
- 반복 횟수인 ```count```는 양의 정수여야 함

## 예시
```Javascript
'abc'.repeat(-1); // RangeError
'abc'.repeat(0); // ''
'abc'.repeat(1); // 'abc'
'abc'.repeat(2); // 'abcabc'
'abc'.repeat(3.5); // 'abcabcabc'(count will be converted to integer)
'abc'.repeat(1/0); // RangeError
```


## 참고
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/repeat
