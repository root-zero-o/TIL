# State 란?
## 1. 개념
- 컴포넌트 내부에서 변경 가능한 데이터를 관리해야할 때 사용
- 값을 저장하거나 변경할 수 있는 객체로, 보통 이벤트와 함께 사용됨
- 두 컴포넌트 간의 ```state```값을 동기화하는 일 혹은 ```state```를 공유하는 일은 그 ```state```값을 필요로 하는 컴포넌트 간의 가장 가까운 공통 조상 컴포넌트로 ```state```를 끌어올리기

## 2. 클래스형 컴포넌트에서 ```state``` 사용하기
- ```state```의 이름과 초기값을 constructor(생성자)에서 설정해주고, render에서 ```this.setState```를 통해 ```state``` 변경 가능
- ```state```값을 변경할 경우, ```this.setState```를 사용해 새로운 값을 줄 수 있음
```javascript
class ClassExample extends React.Component {
  constructor(props) {
    super(props);
    // state 초기값 설정
    this.state = {
      count: 0,
    };
  }

  render() {
    const { count } = this.state;		// state 조회
      return (
        <div>
          <p>You clicked {count} times</p>
          <button onClick={() => {
            this.setState({		// this.setState를 통해 state 업데이트
              count: count + 1
            });
          }}>
            Click me
          </button>
        </div>
      );
    }
  }
}
```
## 3. 함수형 컴포넌트에서 ```state``` 사용하기
- Hook이 추가되면서 함수형 컴포넌트에서도 ```useState```를 통해 ```state```를 사용할 수 있게 됨!
- useState() 사용법은 따로 정리!!

## 참고
- https://chanhuiseok.github.io/posts/react-6/
- https://goddaehee.tistory.com/301
- *useState() 정리해서 링크 걸기!*
