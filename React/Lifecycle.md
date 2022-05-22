# React의 Lifecycle

## 1. Lifecycle이란?
- Lifecycle이란 컴포넌트가 브라우저 상에 나타나고, 업데이트 되고, 사라질 때 호출되는 메서드
- 클래스형 컴포넌트에만 해당됨(함수형 컴포넌트에서는 Hooks 사용)
- 단계
    - Mount : 컴포넌트가 생성되고 웹 브라우저 상에서 나타나는 것
    - Update : props 또는 state의 변경, 부모 컴포넌트의 리렌더링, 강제 렌더링(forceUpdate)
    - Unmount : 컴포넌트가 제거되는 것

## 2. Lifecycle 별 메소드
<br>

<img src="https://user-images.githubusercontent.com/97326130/169683057-8e7b6e54-70f8-4631-b21a-c987f161c46b.png" alt="drawing" width="700"/><
### 1) Mount
- ```constructor```
    - 컴포넌트가 생성될 때 가장 먼저 실행
    - state의 초기 값을 지정할 때 사용
```javascript 
// Class
class Example extends React.Component {
    constructor(props) {
        super(props);
        this.state = { count: 0 };
}

// Hooks
const Example = () => {
    const [count,setCount] = useState(0);
}
```
    
- ```componentWillMount()``` : 컴포넌트가 Mount되기 직전(생성되기 전)에 처리해야 할 일을 넣을 수 있음
- ```render()``` : Mount가 되면서 화면에 그려짐
- ```componentDidMount()``` : 컴포넌트를 생성하고 첫 렌더링을 마친 후 실행되는 메소드


### 2) Update
- ```shouldComponentUpdate()``` : 컴포넌트의 리렌더링 여부를 결정하는 메소드(true or false 반환) 
- ```render()``` : 새로운 값을 사용해 리렌더링
- ```componentDidUpdate()``` : 컴포넌트 업데이트가 끝난 후 실행되는 메소드 / props, state 업데이트에 따라 계속 실행

### 3) Unmount
- ```componentWillUnmount()``` : 컴포넌트를 DOM에서 제거할 때 실행(componentDidMount에서 등록한 이벤트가 있으면 제거해야 함)

## 참고
- [생활코딩 Lifecycle 강의](https://www.youtube.com/watch?v=VgbMW2f5laM)
- https://velog.io/@juy23/React-React-life-cycle
