# JSX: JavaScript XML

JSX는 JavsScript의 확장 문법으로, JavsScript의 모든 기능을 포함하고 있습니다. +HTML 태그를 사용할 수 있습니다.

## JSX, TSX 파일 컴파일 지원

`react-scripts`, `@vitejs/plugin-react-swc`

## JSX는 반드시 하나의 루트 태그로 존재 해야만 하며, 첫글자를 대문자로 작성합니다.

### 가능!

```jsx
const App = () => {
	return (
		<div>
			<h1>Hello, World!</h1>
		</div>
	);
};
```

### 불가능!

```jsx
const App = () => {
	return (
		<div>
			<h1>Hello, World!</h1>
		</div>
    <div>
			<h1>Hello, World!</h1>
		</div>
	);
};
```

그래서, `<></>`를 사용해서 전체를 감싸줍니다. `<React.Fragment></React.Fragment>`와 동일합니다.
음 ... 슈걸씬퉥쓰~?

## HTML5와의 차이점!

`<br/>` 과 같이, 닫는 태그가 필수로 필요하다!

## 표현식을 적용할 수 있습니다.

아래와 같이 `number`라는 변수를 정의한 후, `{}`를 사용하여 넣을 수 있다.

```tsx
const App = () => {
	const number = 100;
	return (
		<>
			<h1>Count: {number}</h1>
		</>
	);
};
export default App;
```

## 조금 특이하게도 `class`라는 속성 대신 `className`이라는 속성을 써야만 합니다.

```tsx
const App = () => {
	const number = 100;
	return (
		<>
			<h1 className='count'>Count: {number}</h1>
		</>
	);
};
export default App;
```
