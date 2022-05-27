# useEffect
## 1. 개념
- React 컴포넌트가 렌더링 될 때마다 특정 작업(Side effect)을 실행할 수 있도록 해주는 리액트 Hook
- 함수형 컴포넌트에서도 Lifecycle 메서드를 사용할 수 있게 해줌!
    - ```componentDidMount```, ```componentDidupdate```, ```componentWillUnmount```가 합쳐진 것으로 생각
- ```useEffect```가 하는 일
    - React에게 컴포넌트가 렌더링 이후에 어떤 일을 수행해야 하는 지를 말함
    - React는 넘긴 함수(이 함수를 ```effect```라 부름)를 기억했다가 DOM 업데이트를 수행한 이후에 불러냄
    - ```useEffect```는 첫 번째 렌더링과 이후 모든 업데이트에서 수행됨(렌더링 이후에 발생)

## 2. 사용방법
- 기본 형태
    - function : 실행하고자 하는 함수
    - deps : 배열 형태. function을 실행시킬 조건(deps에 특정 값을 넣으면 컴포넌트가 mount될 때, 지정한 값이 업데이트될 때 ```useEffect``` 실행
```javascript
useEffect(function, deps)
```

- useEffect 불러오기
```javascript
import React, {useEffect} from "react";
```

### 1) 컴포넌트가 Mount 되었을 때
```javascript
 useEffect(() => {
    console.log("렌더링 될때마다 실행");
  });
```
- deps 부분을 생략한다면 해당 컴포넌트가 렌더링 될 때마다 ```useEffect``` 실행
- 맨 처음 랜더링 될 때 한 번만 실행하고 싶다면 deps 위치에 빈 배열을 넣어줌
```javascript
useEffect(() => {
    console.log("맨 처음 렌더링될 때 한 번만 실행");
  },[]);
```
### 2) 컴포넌트가 Update 되었을 때
```javascript
useEffect(() => {
    console.log(name);
    console.log("name이라는 값이 업데이트 될 때만 실행");
  },[name]);
```
- 특정 값이 업데이트될 때만 실행하고 싶을 때는 deps 위치의 배열 안에 실행 조건을 넣어줌(업데이트 + 마운트 될 때 실행됨)
- 업데이트될 때만 실행시키고 싶으면 아래와 같은 방법 사용
```javascript
const mounted = useRef(false);
  useEffect(() => {
    if (!mounted.current) {
      mounted.current = true;
    } else {
      console.log(name);
      console.log("업데이트 될 때마다 실행");
    }
  }, [name]);
```
### 3) 컴포넌트가 Unmount 되었을 때 + Update 되기 직전에
```javascript
useEffect(() => {
    console.log("컴포넌트 나타남");
    console.log(name);
    return () => {
      console.log("cleanUp 함수");
    };
  });
```
- ```useEffect```는 함수를 반환할 수 있는데, 이 함수를 ```cleanup```이라고 함
- Unmount될 때만 ```cleanup``` 함수를 실행시키고 싶으면 deps에 빈 배열을 넣으면 됨
- 특정 값이 업데이트되기 직전에 ```cleanup```함수를 실행시키고 싶으면 deps에 해당 값을 넣어주면 됨

## 참고
- https://ko.reactjs.org/docs/hooks-effect.html
- https://cocoon1787.tistory.com/796
