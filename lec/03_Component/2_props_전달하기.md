# Props 전달하기

## Greeting 컴포넌트 만들기

```tsx
const Greeting = () => {
	return <h1>Hello, Greeting</h1>;
};

export default Greeting;
```

## APP 컴포넌트에서 사용하기

```tsx
import Greeting from '...';

const App = () => {
	return (
		<>
			<Greeting />
		</>
	);
};

export default App;
```

### 프로퍼티 전달하기

```tsx
interface GreetingProps {
	name: string;
	age: number;
	onSay: () => void;
}

type GreetingProps = {
	name: string;
	age: number;
	onSay: () => void;
};

const Greeting = (props: GreetingProps) => {
	return (
		<h1 onClick={onSay}>
			Hello, {props.name} - {props.age}
		</h1>
	);
};

export default Greeting;
```

```tsx
<Greeting name='John' age={30} onSay={onSay} />
```
