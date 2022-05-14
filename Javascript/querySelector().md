# querySelector()
## 구문
```javascript
document.querySelector(#id); // id값 id를 가진 요소를 찾는다.
document.querySelector(.class); // class값 class를 가진 요소를 찾는다.
```
제공한 선택자 또는 선택자 뭉치와 일치하는 문서 내 첫 번째 element 반환(일치하는 요소가 없으면 ```null``` 반환)
- ```selectors``` : 하나 이상의 선택자를 포함한 DOMstring. 유효한 CSS 선택자여야만 함
- 반환값 : 제공한 CSS 선택자를 만족하는 첫 번째 Element 객체

## 예제
```HTML
<!---HTML--->
<body>
  <div class = "test">
    <h1>Hello Selector</h1>
  </div>
  <script = src="main.js"></script>
</body> 
```

```javascript
//Javacript
const myDiv = document.querySelector(".test"),
        myH1 = myDiv.querySelector("h1");

console.log(myDiv); // <div class="test">...</div>
console.log(myH1); // <h1>Hello Selector</h1>
```

## ```querySelectorAll()```
```querySelector```와 사용 방법은 동일하며, 여러 요소를 한 번에 가져올 수 있음
```javascript
querySelectorAll("#id, .class");
```

## 참고
- https://developer.mozilla.org/ko/docs/Web/API/Document/querySelector
- https://kyounghwan01.github.io/blog/JS/JSbasic/queryselector/
- https://junlab.tistory.com/13
