# filter()
```javascript
Array.filter(callback(element, index, array))
```
배열을 순회하며 요소마다 조건을 확인한 후 만족하는 원소들로 구성된 새로운 배열 리턴
- ```callback``` : 각 요소를 시험할 함수. true를 반환하면 요소를 유지하고, false를 반환하면 버림
- ```element``` : 처리할 현재 요소
- ```index``` : 처리할 요소의 인덱스
- ```array``` : ```filter```를 호출한 배열
```javascript
let numbers = [1, 4, 9]
let parameters = numbers.filter((num, index, arr) =>
          	{console.log(num, index, arr)})
// 결과
1 0 [ 1, 4, 9 ]
4 1 [ 1, 4, 9 ]
9 2 [ 1, 4, 9 ]
```
## 예제
```javascipt
let users = [
  { id: 85, name: 'William', age: 34, group: 'editor' },
  { id: 97, name: 'Oliver', age: 28, group: 'admin' }
];
let res = users.filter(it => it.name.includes('oli'))  //간단한 검색

let res = users.filter(it => new RegExp('oli', "i").test(it.name));

let arrA = [1, 4, 3, 2];
let arrB = [5, 2, 6, 7, 1];
arrA.filter(it => arrB.includes(it)); //A,B의 교집합 구하기
```

## 참고
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/filter
- https://velog.io/@tjdud0123/javascript-map-filter-%ED%95%A8%EC%88%98
