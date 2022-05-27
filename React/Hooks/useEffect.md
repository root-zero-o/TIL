# useEffect
## 1. 개념
- React 컴포넌트가 렌더링 될 때마다 특정 작업(Side effect)을 실행할 수 있도록 해주는 리액트 Hook
- 함수형 컴포넌트에서도 Lifecycle 메서드를 사용할 수 있게 해줌!
    - ```componentDidMount```, ```componentDidupdate```, ```componentWillUnmount```가 합쳐진 것으로 생각
- ```useEffect```가 하는 일
    - React에게 컴포넌트가 렌더링 이후에 어떤 일을 수행해야 하는 지를 말함
    - React는 넘긴 함수(이 함수를 ```effect```라 부름)를 기억했다가 DOM 업데이트를 수행한 이후에 불러냄
    - ```useEffect```는 첫 번째 렌더링과 이후 모든 업데이트에서 수행됨(렌더링 이후에 발생)
 - ```useEffect```안에서 사용하는 상태나, props가 있다면 ```useEffect```의 deps에 넣어주어야 함(그렇지 않으면 ```useEffect```에 등록한 함수가 실행될 때 최신 props/state를 가리키게 되지 않음

## 2. 사용방법
- 기본 형태
    - function : 실행하고자 하는 함수
    - deps : 배열 형태. function을 실행시킬 조건(deps에 특정 값을 넣으면 컴포넌트가 mount될 때, 지정한 값이 업데이트될 때 ```useEffect``` 실행
```javascript
useEffect(() => {
    // 마운트 시 작업 설정

    return() => {
        // 언마운트
        // 반환되는 함수는 cleanup함수(뒷정리)
        // deps가 비어있는 경우에는 컴포넌트가 사라질 때 cleanup함수 호출
    }
}, [deps]);
```

- useEffect 불러오기
```javascript
import React, {useEffect} from "react";
```

- deps에 빈 배열
    - 처음 컴포넌트 마운트 됐을 때 ```useEffect```내 함수 호출(componentDidmount)
    - 컴포넌트가 언마운트 될 때 cleanup 함수 호출(componentWillUnmount)
- deps에 의존 값 존재
    - 처음 컴포넌트가 마운트 됐을 때 ```useEffect```내 함수 호출(componentDidmount)
    - 의존 값이 업데이트 됐을 때(componentDidUpdate)
    - 컴포넌트가 언마운트 될 때 cleanup 함수 호출(componentWillUnmount)
- 아예 파라미터를 안 넣었을 경우 : 리렌더링 될 떄마다 함수 호출



## 참고
- https://ko.reactjs.org/docs/hooks-effect.html
- https://cocoon1787.tistory.com/796
