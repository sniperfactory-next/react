# CSS 사용하는 방법

## assets/globals.css 파일

전역적으로 적용되는 CSS 파일입니다. 어디에 임포트 하던지 전역으로 적용되지만, 관례적으로 가장 상위인 main.tsx 파일 안에서 불러옵니다.

## [컴포넌트 이름].module.css 파일

컴포넌트 파일이 있는 위치에 만드는 것이 관례입니다.

이런 이름으로 만든 css 파일은 특정 컴포넌트에서 사용할 스타일만 정의할 수 있으며, 이 모듈로 정의하는 경우에는, id, class 선택자 한개만 사용할 수 있습니다. 또한, 자식 선택자는 사용할 수 없습니다.

딱히 module.css 라는 이름 자체에 기능이 있는것은 아니고, 이렇게 파일 이름을 작성하면 이 컴포넌트에서만 쓰겠구나! 하는 암묵적인 관례이다.

```css
.title {
	font-size: 20px;
	color: blue;
}
```

```jsx
import styles from './Component.module.css';

const Component = () => <h1 className={styles.title}></h1>;
```

## CSS-in-JS

module.css 파일의 기능, 즉, 컴포넌트에서만 사용하는 그런 기능들을 자동적으로 탑재하고 있습니다.

대표적으로, Styled Components, Emotion, Vanilla Extract 등이 있습니다.

하지만, 어떤 태그를 쓰는지 찾기 힘들기 때문에 HTML코드의 태그 구조의 가독성이 상당히 떨어진다는 단점이 있습니다.

이런 라이브러리들은 자바스크립트로 CSS를 적용하자고 하는 공통적인 목적을 가지고 있다.

### Styled Components

```tsx
import styled from 'styled-components';

const App = () => {
	const Title = styled.h1`
		color: red;
	`;
	return (
		<>
			<Title>Hello World!</Title>
		</>
	);
};
```

### Emotion

Styled Components에서 지원하지 않는 것들을 지원합니다.

IE 11을 지원한다는 것인데요 ..., 아직까지도 사용하는 사람이 상당히 많기 때문에 사용하기도 합니다.

태그에 대한 가독성을 해결한 경우입니다. css를 사용하고, 태그를 그대로 사용하도록 제공했습니다.

```jsx
import {css} from '@emotion/css';

const App = () => {
	return (
		<div>
			<h1
				className={css`
					font-size: 30px;
					color: #ed4848;
					text-decoration: line-through;
					&:hover {
						color: blue;
					}
				`}
			>
				Hello, World!
			</h1>
		</div>
	);
};

export default App;
```

### Vanilla Extract

제로 런타임이 도입됨. CSS계산을 위해 들어가는 비용이 거의 없다.
최근에 주목받고 있는 방법이기는 하다.

#### 설치하기

```sh
npm i @vanilla-extract/css @vanilla-extract/vite-plugin
```

#### 스타일 파일 생성하기

```ts
import {style} from '@vanilla-extract/css';

export const h1Style = style({
	fontSize: '30px',
	color: '#ed3838',
	textDecoration: 'line-through',
});
```

#### 스타일 파일 불러와서 사용하기

```tsx
import {h1Style} from './vanila/styles.css.ts';
const App = () => {
	return (
		<div>
			<h1 className={h1Style}>Hello, World!</h1>
		</div>
	);
};

export default App;
```

#### 환경설정 파일 수정하기(vite.config.js)

```ts
import {defineConfig} from 'vite';
import react from '@vitejs/plugin-react-swc';
import {vanillaExtractPlugin} from '@vanilla-extract/vite-plugin';

export default defineConfig({
	plugins: [react(), vanillaExtractPlugin()],
});
```
