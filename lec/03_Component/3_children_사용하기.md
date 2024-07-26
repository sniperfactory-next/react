# children 사용하기

## children 속성은 컨텐츠 자체를 전달한다. 따라서 h1 태그까지 전달하게 된다.

```tsx
const Container = (props: {children: React.ReactNode}) => {
	return <div>{children}</div>;
};
```

```tsx
const App = (props: {children: React.ReactNode}) => {
	return (
		<Container>
			<h1>Hello World</h1>
		</Container>
	);
};
```
