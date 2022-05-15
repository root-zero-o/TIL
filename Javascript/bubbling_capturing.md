# 버블링(bubbling)과 캡쳐링(capturing)
## 1. 버블링(bubbling)
### 1) 버블링이란?
특정 화면 요소에서 이벤트가 발생했을 때 해당 이벤트가 더 상위의 화면 요소들로 전달되어 가는 특성으로, <br>
브라우저가 이벤트를 감지하는 방식 때문에 나타나는 현상
- 브라우저는 특정 화면 요소에서 이벤트가 발생했을 때 그 이벤트를 최상위에 있는 화면 요소까지 전파시키기 때문
- 각 태그마다 이벤트가 등록되어 있기 때문에 발생(이벤트가 특정 ```<div>```에만 달려있다면 버블링이 일어나지 않음
- 버블링과 캡처링은 ```stopPropagation()```으로 막을 수 있음

### 2) 예제
#### HTML
```html
<body>
	<div class="one">
		<div class="two">
			<div class="three">
			</div>
		</div>
	</div>
</body>

```
#### Javascript
```javascript
var divs = document.querySelectorAll('div');
divs.forEach(function(div) {
	div.addEventListener('click', logEvent);
});

function logEvent(event) {
	console.log(event.currentTarget.className);
}
```
- 세 개의 ```<div>```에 모두 클릭 이벤트를 등록하고 클릭 했을 때 ```logEvent``` 함수를 실행시키는 코드
- 최하위 div 태그인 ```<div class="three"></div>```를 클릭하면 콘솔에 three - two - one 이 차례로 찍힘!

## 2. 캡처링(capturing)
### 1) 캡쳐링이란?
이벤트 버블링과 반대방향으로, 즉 이벤트가 하위 요소로 전파되는 것
- 캡쳐링 단계를 이용해야 하는 경우는 흔치 않음(추후 추가 정리 예정)

## 참고
- https://ko.javascript.info/bubbling-and-capturing
- https://joshua1988.github.io/web-development/javascript/event-propagation-delegation/
- [TIL - preventDefault(), stopPropagation()](https://github.com/yyeonggg/TIL/blob/master/Javascript/preventDefault()_stopPropagation().md)
