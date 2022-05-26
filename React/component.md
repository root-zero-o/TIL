# 컴포넌트(Component)
## 1. 개념
- 컴포넌트 : ```props```를 input으로 하고, UI가 어떻게 보여야 하는지 정의하는 함수
- UI를 구성하기 위해서는 화면에 컴포넌트를 그리고(Mounting), 갱신하고(Updating), 지워야(Unmounting) 함
- 컴포넌트는 두 가지 인스턴스 속성(```props```, ```state```)을 가짐
    - ```props```는 컴포넌트의 mounting, updating 프로세스 시점에 값이 할당될 뿐, 컴포넌트 내부에서 값을 변경할 수 없음
    - 상황에 따라 변경되어야 하는 값들은 ```state``` 이용
- 🤷‍♂️왜 ```props```와 ```state```가 나뉘는거지?
    - 컴포넌트 간에는 무조건 ```props```를 통해서만 데이터를 주고 받고, ```props```는 컴포넌트 내부에서 변경되지 않는다! 따라서 한쪽 방향으로만 고민하면 된다!😀
    - Updating을 할지 결정하는 ```shouldComponentUpdate()``` 함수에서 ```state```만 비교하면 됨!

## 2. ```setState()``` API

- 컴포넌트의 ```state```를 변경할 때 사용하는 API
- 🤷‍♂️왜 ```state```를 직접 변경하지 않고 굳이 API로 변경하지?
    - JavaScript의 비교 연산자는 피연산자의 값이 아닌 reference 값을 기준으로 참/거짓을 리턴하기 때문!
    - ```state```의 값을 직접 변경할 경우, 해당 오브젝트의 ```reference```값이 변하지 않아 컴포넌트는 ```state```가 변경되지 않았다고 인식
    - 따라서 ```setState```를 이용해 ```state```의 변경 가능성을 명시적으로 알려줌
```javascript
let a = { name : 'babo' };
let b = { name : 'babo' };
let c = { name : 'babo' };
let d = c;
console.log(a === b, c === d); // false true 
```
- ```setState```호출 즉시 ```state```가 즉시 갱신되는 것이 아니라 비동기로 동작함 !!
    - 상태가 변경된 직후에 필요한 작업이 있다면 ```setState(nextState, callback)```의 ```callback```을 사용해야 함
    - 비동기로 동작하게 되면 ```render``` 시점과 별개로 동작하기 때문에 자연스러운 갱신이 가능함

## 3. 종류
### 1) 함수형 컴포넌트
function으로 정의하고 return문에 jsx코드 반환
```javascript
import React from "react";
import "./App.css";

const NameBox = () => {
  const name = "test";
  return <div>{name}</div>;
};

export default NameBox;
```
### 2) 클래스형 컴포넌트
class로 정의하고 ```render()``` 함수에서 jsx코드 반환
```javascript
import React, { Component } from "react";

class NameBox extends Component {
  render() {
    const name = "react";
    return <div className="react">{name}</div>;
  }
}

export default NameBox;
```
- 클래스형 컴포넌트에서는 state(상태)를 사용할 수 있음
- 라이프사이클 및 메서드를 이용해 조작을 할 수 있음(함수형에서도 hook을 사용해 구현 가능)
    
## 참고
- [⭐컴포넌트란 무엇인지 잘 정리되어 있는 글](https://medium.com/little-big-programming/react%EC%9D%98-%EA%B8%B0%EB%B3%B8-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EB%A5%BC-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90-92c923011818)
- https://chanhuiseok.github.io/posts/react-4/
