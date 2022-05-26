# Props
## 1. Props(Properties)란?
- 상위 컴포넌트가 하위 컴포넌트에 값을 전달할 때 사용(단방향 데이터 흐름을 가짐)
- ```props```는 수정할 수 없음!(읽기 전용 데이터)
- ```props```를 받는 함수형 컴포넌트에 인자를 정의하면, ```props```를 속성으로 가지는 객체가 인자로 전달됨

## 2. 사용방법
- 프로퍼티에 문자열을 전달할 때는 큰 따옴표(```""```)를, 문자열 외의 값을 전달할 때는 중괄호(```{}```) 사용

#### App.js
```javascript

import React, { Component } from 'react';
import Header from './component/Header';
import Footer from './component/Footer';
import Main from './component/Main';

function App() {
  return (
    <div>
      <Header />
      <Main name="근영" color="blue" score={100}/> //n개의 프로퍼티 전달 가능, 숫자열은 중괄호 사용
      <Footer />
    </div>
  );
}

export default App;
```
#### Main.js
```javascript
import React from 'react';

function Main(props) { //props 대신 {name, color}라는 비구조화 할당 가능
    return (
        <div>
            <main>
                <h1 style={{color: props.color}}>안녕하세요. {props.name} 입니다.</h1>
            </main>
        </div>
    );
}

export default Main;
```

## 3. props의 자료형, 타입 정의
- ```props```의 자료형을 미리 선언할 수 있음
- 리액트가 ```props```로 전달하는 값을 효율적으로 알 수 있고, 버그 예방에 도움이 됨
- 리액트에서 제공하는 ```prop-types```를 이용해 자료형 선언
```javascript
import PropTypes from 'prop-types'; //props 타입 지정을 위해 사용

class Greeting extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}
// props 타입 지정
Greeting.propTypes = {
  name: PropTypes.string
};
```
## 4. 불리언 프로퍼티 사용하기
- true, false만 정의 가능한 자료형
- 중괄호로 감싸 전달할 필요 없이 프로퍼티 이름만 선언하면 됨
#### Main.js
```javascript
import React from 'react';
import PropTypes from 'prop-types'

function Main({color, name, maleYn}) {
    const msg = maleYn ? '남자' : '여자'; // 불리언 사용
    return (
        <div>
            <main>
                <h1 style={{color}}>안녕하세요. {name} 입니다. ({msg})</h1>
            </main>
        </div>
    );
}

Main.propTypes = {
    name: PropTypes.string
}

Main.defaultProps = {
    name: '디폴트'
}

export default Main;
```
#### App.js
```javascript
import React, { Component } from 'react';
import Header from './component/Header';
import Footer from './component/Footer';
import Main from './component/Main';
import Wrapper from './component/Wrapper';

function App() {
  return (
    <div>
      <Header />
      <Main name="근영" color="blue" maleYn/> // "안녕하세요 근영입니다. (남자)" 가 출력됨(maleYn이 없으면 여자 출력)
      <Footer />
    </div>
  );
}

export default App;
```

## 5. ```props.children``` 활용하기
#### App.js
```javascript
import React, { Component } from 'react';
import Header from './component/Header';
import Footer from './component/Footer';
import Main from './component/Main';
import Wrapper from './component/Wrapper';

function App() {
  return (
    <div>
      <Header />
      <Wrapper> // Main 컴포넌트를 Wrapper로 감싸줌
        <Main color="blue"/>
      </Wrapper>
      <Footer />
    </div>
  );
}

export default App;
```

#### Wrapper.js
```javascript
import React from 'react';

function Wrapper(props) {
    const style = {
        backgroundColor: 'yellow',
      };
    
    return (
        <div style={style}>
            {props.children} // props.children 렌더링하면 Main컴포넌트의 배경색이 노란색이 됨!
        </div>
    );
}

export default Wrapper;
```

## 참고
- https://goddaehee.tistory.com/300
- https://ko.reactjs.org/docs/components-and-props.html
- https://velog.io/@soyi47/React-Component-props-state
