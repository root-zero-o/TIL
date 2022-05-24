# **JSX (JavaScript XML)**
## 1. JSX 란?
- JavaScript에 XML을 추가한 확장된 문법(공식적인 JavaScript 문법은 아님)
- 브라우저에서 실행하기 전에 바벨*을 사용하여 일반 JavaScript 형태의 코드로 변환됨
- 하나의 파일에 JavaScript와 HTML을 동시에 작성하여 편리함(가독성이 높고, 작성하기 편리함)
<br><br>
*바벨(Babel): JavaScript ES6문법을 ES5로 변환해주는 트랜스파일러. 이를 통해 React를 일반 브라우저에서 실행시킬 수 있음*

----

## 2. JSX 문법
### 1) 반드시 부모 요소 하나가 감싸는 형태여야 함
- 가상돔(Virtual DOM)에서 컴포넌트 변화를 감지할 때 효율적으로 비교할 수 있도록 컴포넌트 내부는 하나의 DOM 트리 구조로 이루어져야 함
```javascript
function App() {
	return (
		<>
			<div>I Love</div>
			<div>JavaScript!</div>
		</>
	);
}
```
### 2) JavaScript 표현식
- JSX 안에서 JavaScript 표현식을 사용할 수 있음
- JavaScript 표현식을 작성하려면 JSX 내부에서 코드를 ```{}```로 감싸주면 됨
- 유효한 모든 JavaScript 표현식을 넣을 수 있음
```javascript
function App() {
	const name = 'GeunYeong';
	return (
		<div>
			<div>Hello</div>
			<div>{name}!</div>
		</div>
	);
}
```
### 3) ```if```문(```for```문) 대신 삼항연산자(조건부 연산자) 사용
- ```if```문과 ```for```반복문은 JavaScript 표현식이 아니기 때문에 JSX 내부 Javascript 표현식에서는 사용 불가
- 따라서 JSX 주변 코드에서 ```if```문을 사용하거나, ```{}```안에서 삼항연산자(조건부연산자) 사용
#### 방법1 : 외부에서 사용
```javascript
function App() {
	let desc = '';
	const loginYn = 'Y';
	if(loginYn === 'Y') {
		desc = <div>김근영 입니다.</div>;
	} else {
		desc = <div>바보 입니다.</div>;
	}
	return (
		<>
			{desc}
		</>
	);
}
```
#### 방법2 : AND연산자(```&&```) 사용
```javascript
// 조건이 만족하지 않을 경우 아무것도 노출되지 않는다.
function App() {
	const loginYn = 'Y';
	return (
		<>
			<div>
				{loginYn === 'Y' && <div>근영 입니다.</div>}
			</div>
		</>
	);
}
```
#### 방법 3 : 즉시실행함수 사용
```javascript
function App() {
	const loginYn = 'Y';
	return (
		<>
			{
			  (() => {
				if(loginYn === "Y"){
				  return (<div>GodDaeHee 입니다.</div>);
				}else{
				  return (<div>비회원 입니다.</div>);
				}
			  })()
			}
		</>
	);
}
```
### 4) React DOM은 camelCase 프로퍼티 명명 규칙을 사용함
#### a. JSX 스타일링
- JSX에서 JavaScript 문법을 쓰려면 ```{}```을 써야 하기 때문에, 스타일을 적용할 때에도 객체 형태로 넣어주어야 함
- 카멜 표기법으로 작성해야 함
```javascript
function App() {
	const style = {
		backgroundColor: 'green',
		fontSize: '12px'
	}
	return (
		<div style={style}>Hello, 근영!</div>
	);
}
```
#### b. class 대신 ```className``` 사용
```javascript
function App() {
	const style = {
		backgroundColor: 'green',
		fontSize: '12px'
	}
	return (
		<div className="testClass">Hello, 근영!</div>
	);
}
```
### 5) JSX 내에서 주석 사용 방법
- ```{/*... */}```의 방법을 사용

----
## 참고
- https://goddaehee.tistory.com/296
- https://ko.reactjs.org/docs/introducing-jsx.html
