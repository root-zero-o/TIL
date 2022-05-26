# 이벤트(Event)
## 1. 개념
- 프로그래밍하고 있는 시스템에서 일어나는 사건(action) 혹은 발생(occurrence)
- 각각의 이용가능한 이벤트들은 이벤트 핸들러(event handler)를 가지고 있음
- 이벤트 핸들러는 이벤트가 발생되면 실행되는 코드 블럭

## 2. 이벤트 객체
- 이벤트 함수 내의 객체(보통 event 등의 이름으로 명명된 파라미터)
- 이벤트 객체는 추가적인 기능과 정보를 제공하기 위해 이벤트핸들러에 자동으로 전달됨
```javascript
function bgChange(e) {
  const rndCol = 'rgb(' + random(255) + ',' + random(255) + ',' + random(255) + ')';
  e.target.style.backgroundColor = rndCol;
}

btn.addEventListener('click', bgChange);
```
- 이벤트 객체의 target 프로퍼티는 항상 이벤트가 발생된 요소, type 프로퍼티는 이벤트 타입을 나타냄
- 모든 이벤트 객체는 type와 target 프로퍼티를 가지고, 이벤트 리스너(이벤트 핸들러)가 호출될 때 인수로 전달됨
- ```addEventListener()```메소드를 사용하면 하나의 이벤트 타입에 여러 개의 이벤트 리스너 등록 가능
