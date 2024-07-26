# Context API

컴포넌트의 깊이가 깊어질수록 프로퍼티를 안으로 전달해야하는데, 이렇게 여러번 전달해야하는 비효율적인 과정을 프롭스드릴링 이라고 한다. 이러한 프롭스 드릴링을 해결하기 위해서 나온 것이 Context API 이다.

```tsx
import {createContext, useState} from 'react';
import Page from './components/learn/Page';

export const CounterContext = createContext<{
	count: number;
	setCount: React.Dispatch<React.SetStateAction<number>>;
}>({
	count: 0,
	setCount: () => {},
});

const App = () => {
	const [count, setCount] = useState(0);
	return (
		<>
			<CounterContext.Provider value={{count, setCount}}>
				<Page count={count} setCount={setCount} />
			</CounterContext.Provider>
		</>
	);
};
export default App;
```

이제 이 컨텍스트가 공급하는 값을 하위 컴포넌트 내부에서 가져와서 쓸 수 있다.

```tsx
import {useContext} from 'react';
import {CounterContext} from '../../App';

const DisplayCounter = () => {
	const {count} = useContext(CounterContext);
	return (
		<>
			<h1>Count: {count}</h1>
		</>
	);
};
export default DisplayCounter;
```

이처럼 아무런 기능도 없이 보여주기만하는 컴포넌트인 DisplayCounter와 같은 컴포넌트를 프레젠테이셔널 컴포넌트라고 합니다.

## Context API를 쓰지도 않는데 리렌더링이 되는 경우가 있다.

Context.Provider 하위 컴포넌트인 경우에 발생하는 현상이다. 이러한 경우에는 리렌더링을 방지하기 위해 메모이제이션이 필요하다.

따라서, Context API와 무관한 컴포넌트에 대해서는 React.memo를 통해서 리렌더링을 방지해야 한다.

## Context API를 효율적으로 관리하기 위한 파일 (counterContext.tsx)

```tsx
export const CounterContext = createContext<{
	count: number;
	setCount: React.Dispatch<React.SetStateAction<number>>;
}>({
	count: 0,
	setCount: () => {},
});

export const CounterContextProvider = ({
	children,
}: {
	children: React.ReactNode;
}) => {
	const [count, setCount] = useState(0);
	return (
		<CounterContext.Provider value={{count, setCount}}>
			{children}
		</CounterContext.Provider>
	);
};
```

이어서, 앱 컴포넌트에서는 이렇게 사용할 수 있다.

```tsx
const App = () => {
	return (
		<>
			<CounterContextProvider>
				<Page />
			</CounterContextProvider>
		</>
	);
};
```

QUESTION 이렇게 처리를 하면, Page 컴포넌트에 프로퍼티를 직접 전달하지 않기 때문에 메모이제이션 최적화 비용이 사라진다?

왜?

컨텍스트를 고차함수 상태로 변경했기 때문이다. 컴포넌트 안에서 다른 컴포넌트를 반환하는 리액트 메모와 같은 방식으로 코드를 작성했기 때문이다.
따라서, 별도로 처리를 하지 않아도 리액트 메모가 자동으로 적용이 되었다고 판단할 수 있다.

왜 고차함수면 메모이제이션이 적용되는가요?

고차 컴포넌트가 가지는 특징이라고 이해할 수 있다.

그러면 고차 컴포넌트가 내부에서 어떻게 동작하는걸까 ... ? ... -> 알면 좋아~
