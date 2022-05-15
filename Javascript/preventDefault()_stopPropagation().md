# preventDefault(), stopPropagation()
## 1. preventDefault()
### 1) preventDefault()란?
```javascipt
event.preventDefault();
```
해당 이벤트에 대한 사용자 에이전트의 기본 동작을 실행하지 않도록 지정함
- 취소 불가능한 이벤트의 경우 ```preventDefault()```를 호출해도 아무 효과가 나타나지 않음
- 이벤트가 전파되는 것(버블링, 캡쳐링)을 중지시키지는 않음 <br>
*버블링 : 자식 element에서 발생된 event가 부모 element 순으로 전달되는 현상* <br>
*캡처링 : 부모 element에서 발생된 event가 자식 element 순으로 전달되는 현상*

### 2) 예제
#### HTML
```html
<body>
        <form id="login-form">
            <input required maxlength="15" type="text" placeholder="What is your name?"/>
            <input type="submit" value="Log In"/>
        </form>
        <script = src="app.js"></script> 
    </body>       
```
#### Javascript
```javascript
function onLoginSubmit(event){
    event.preventDefault();
    console.log(event);
}

loginForm.addEventListener("submit", onLoginSubmit)
```
- 위의 예시에서 ```preventDefault()```로 인해 ```submit```으로 인해 더이상 자동으로 새로고침이 되지 않음

## stopPropagation()
### stopPropagation()이란?
```javascipt
event.stopPropagation();
```
현재 이벤트가 캡처링/버블링 단계에서 더 이상 전파되지 않도록 방지함(이벤트 전파 중단)
- 이벤트의 기본 동작은 실행되므로, 링크나 버튼의 클릭을 막는 것은 아님

## 참고
- https://developer.mozilla.org/ko/docs/Web/API/Event/preventDefault
- https://pa-pico.tistory.com/20
- https://developer.mozilla.org/ko/docs/Web/API/Event/stopPropagation
- [TIL - 이벤트 버블링과 캡처링](https://github.com/yyeonggg/TIL/blob/master/Javascript/bubbling_capturing.md)
