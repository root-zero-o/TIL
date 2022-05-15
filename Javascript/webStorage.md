# 웹스토리지
## 1. 웹 스토리지(Web Storage)란?
### 1) 개념
- 브라우저 상에 데이터를 저장할 수 있는 기술
- 저장해야 할 데이터가 별로 중요하지 않거나, 유실되어도 무방할 데이터일 때 사용
### 2) 종류
- 세션 스토리지(sessionStorage) 
    - 웹페이지의 세션이 끝날 때 저장된 데이터가 지워짐
    - 브라우저에서 같은 웹사이트를 여러 탭이나 창에 띄우면, 여러 개의 세션 스토리지에 데이터가 서로 격리되어 저장되며, 각 탭이나 창이 닫힐 때 저장해 둔 데이터도 함께 소멸
- 로컬 스토리지(localStorage) : 웹페이지의 세션이 끝나도 데이터가 지워지지 않음
    - 여러 탭이나 창 간에 데이터가 서로 공유되며, 탭이나 창을 닫아도 데이터는 브라우저에 남아있음
    - 로컬스토리지의 데이터 영속성(persistence)은 동일한 컴퓨터에서 동일한 브라우저를 사용할 때만 해당함
### 3) 특징
- 키(key)와 값(value)으로 이루어진 데이터를 저장할 수 있음
- 오직 문자형(string) 데이터만 저장할 수 있어, 다른 타입의 데이터를 저장하려고 할 때 문자형으로 변환 👉 이를 해결하기 위해 JSON 형태로 데이터를 읽고 씀

## 2. 로컬 스토리지(localStorage)
### 구문
```javascript
mystorage = window.localStorage;
```
- 항목 추가
```javascipt
localStorage.setItem('myCat','Tom');
```
- 항목 읽기
```javascript
const cat = localStorage.getItem('myCat');
``` 
- 항목 제거
```javascript
localStorage.removeItem('myCat');
```
- localStorage 항목의 전체 제거
```javascript
localStorage.clear();
```

## 3. 세션 스토리지(sessionStorage)
### 구문
```javascript
myStorage = window.sessionStorage;
```
- 항목 추가
```javascript
sessionStorage.setItem('myCat', 'Tom');
```
- 자동저장된 내용을 복구하여 내용이 사라지지 않게 하기
```javascript
// 추적할 텍스트 입력 칸 가져오기
let field = document.getElementById("field");

// 자동저장 값이 존재하는지 판별
// (의도치 않게 페이지를 새로 불러올 경우에만 발생)
if (sessionStorage.getItem("autosave")) {
  // 입력 칸의 콘텐츠 복구
  field.value = sessionStorage.getItem("autosave");
}

// 텍스트 입력 칸의 변화 수신
field.addEventListener("change", function() {
  // 결과를 세션에 저장
  sessionStorage.setItem("autosave", field.value);
});
```

## 참고
- https://www.daleseo.com/js-web-storage/
- https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API
- https://developer.mozilla.org/ko/docs/Web/API/Window/localStorage
- https://developer.mozilla.org/ko/docs/Web/API/Window/sessionStorage
