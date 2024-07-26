# form 태그

form 태그를 쓰는 이유는, `웹 표준`에 맞춰주기 위해서 사용한다.

## 로그인 이벤트를 정의

```tsx
const App = () => {
	const login = (e: React.FormEvent<HTMLFormElement>) => {
		e.preventDefault();
		console.log('로그인');
	};
	return (
		<>
			<form action='' onSubmit={login}>
				<input type='text' placeholder='이메일' />
				<input type='text' placeholder='패스워드' />
				<button type='button' onClick={login}>
					로그인하기
				</button>
			</form>
		</>
	);
};
export default App;
```

## e.preventDefault() 함수로 기본 이벤트를 취소하고, 로그인 이벤트를 정의

장점은 따로 처리하지 않아도 엔터키를 활용해서도 요청을 넘길 수 있다. 따라서, submit으로 처리해주는것이 훨씬 좋다.

`e.preventDefault`를 사용하면, submit의 고유 이벤트를 막고 우리가 원하는 로직을 실행하기 위함이다.

```tsx
const App = () => {
	const login = (e: React.FormEvent<HTMLFormElement>) => {
		e.preventDefault();
		console.log('로그인');
	};
	return (
		<>
			<form action='' onSubmit={login}>
				<input type='text' placeholder='이메일' />
				<input type='text' placeholder='패스워드' />
				<button type='submit'>로그인하기</button>
			</form>
		</>
	);
};
export default App;
```
