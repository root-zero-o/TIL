# useRef
## 1. 개념
- DOM을 직접 선택해야 하는 상황에서 ```ref```사용, ```ref```를 사용할 때에는 ```useRef```라는 Hook 함수 사용
- 리액트에서는 ```state```값이 변할 때마다 렌더링 됨 👉 함수 내부 변수들이 기존에 저장하고 있는 값들이 초기화됨 👉 이러한 문제를 해결하기 위해 ref 사용
- ```useRef``` 함수는 ```current``` 속성을 가지고 있는 객체를 반환
- 인자로 넘어온 초기값을 ```current``` 속성에 할당함
- ```current``` 속성은 값을 변경해도 렌더링 되지 않고, 컴포넌트가 렌더링될 때 값이 유실되지 않음 <br><br>


## 2. 사용방법
- 사용하기 위해 import
```javascript
import React, { useState, useRef } from 'react';
```
- 어떤 상자📦에 ref를 담을까요?
```javascript
const nameInput = useRef(); // nameInput이라는 상자에 담을래요
```
- 상자📦안에 어떤게 들어가나요?
```javascript
return (
    <div>
      <input
        name="name"
        placeholder="이름"
        onChange={onChange}
        value={name}
        ref={nameInput}  // 이 input을 상자에 담아주세요
      />
      </div>
   )
```
- 이 상자📦로 무엇을 할까요?
```javascript
const onReset = () => {
    setInputs({
      name: '',
      nickname: ''
    });
    nameInput.current.focus(); // 상자 안에 담긴 친구(nameInput.current)를 focus 해주세요
  };
```
## 3. useRef로 컴포넌트 안의 변수 만들기
- ```useRef```는 컴포넌트 안에서 조회 및 수정할 수 있는 변수를 관리할 때에도 사용됨
- ```useRef```로 관리하는 변수는 값이 바뀌어도 리렌더링X
- ```state```는 함수를 호출하고 나서 그 다음 렌더링 이후로 업데이트 상태 조회 가능, ```useRef```로 관리하는 변수는 설정 후 바로 조회 가능
- ```useRef```로 어떤 값을 관리해요?
    - ```setTimeout```,```setInterval```을 통해 만들어진 ```id```
    - 외부 라이브러리를 사용해 생성된 인스턴스
    - scroll 위치




## 참고
- [벨로퍼트 모던 리액트](https://react.vlpt.us/basic/10-useRef.html)
- https://www.daleseo.com/react-hooks-use-ref/
