# DOM 만들기

## createElement 사용해서 HTML 만들기

```tsx
import {createElement} from 'react';

const App = () => {
	return createElement('h1', null, 'Hello, CreateElement!');
};
```

### 속성을 추가하고 싶다면?

`id`와 `class`속성을 추가하고 싶다면, 아래와 같이 두번째 인자로 넣어주면 됩니다.

```tsx
import {createElement} from 'react';

const App = () => {
	return createElement(
		'h1',
		{id: 'title', class: 'main'},
		'Hello, CreateElement!'
	);
};
```

### 하위 태그를 만들기 위해서는?

```html
<div>
	<h1>Hello, CreateElement!</h1>
</div>
```

```tsx
import {createElement} from 'react';

const App = () => {
	return createElement(
		'div',
		null,
		createElement('h1', null, 'Hello, CreateElement!')
	);
};
```

### 하위 태그를 여러개 만들기 위해서는?

```html
<div>
	<h1>Hello, CreateElement!</h1>
	<p>Hello~~~~~</p>
</div>
```

```tsx
import {createElement} from 'react';

const App = () => {
	return createElement(
		'div',
		null,
		createElement('h1', null, 'Hello, CreateElement!'),
		createElement('p', null, 'Hello~~~~~')
	);
};
```

## 예제 따라하기

```html
<div>
	<header>
		<h1>내 웹사이트</h1>
	</header>

	<nav>
		<ul>
			<li><a href="#section1">소개</a></li>
			<li><a href="#section2">서비스</a></li>
			<li><a href="#section3">연락처</a></li>
		</ul>
	</nav>

	<main>
		<section id="section1">
			<h2>소개</h2>
			<p>여기에 소개 내용을 작성하세요.</p>
		</section>
		<section id="section2">
			<h2>서비스</h2>
			<p>여기에 제공하는 서비스 내용을 작성하세요.</p>
		</section>
		<section id="section3">
			<h2>연락처</h2>
			<p>여기에 연락처 정보를 작성하세요.</p>
		</section>
	</main>

	<footer>
		<p>&amp;copy; 2024 내 웹사이트. 모든 권리 보유.</p>
	</footer>
</div>
```

```tsx
import {createElement} from 'react';

const App = () => {
	return createElement(
		'div',
		null,
		createElement('header', null, createElement('h1', null, '내 웹사이트')),
		createElement(
			'nav',
			null,
			createElement(
				'ul',
				null,
				createElement(
					'li',
					null,
					createElement('a', {href: '#section1'}, '소개')
				),
				createElement(
					'li',
					null,
					createElement('a', {href: '#section2'}, '서비스')
				),
				createElement(
					'li',
					null,
					createElement('a', {href: '#section3'}, '연락처')
				)
			)
		),
		createElement(
			'main',
			null,
			createElement(
				'section',
				{id: 'section1'},
				createElement('h2', null, '소개'),
				createElement('p', null, '여기에 소개 내용을 작성하세요.')
			),
			createElement(
				'section',
				{id: 'section2'},
				createElement('h2', null, '서비스'),
				createElement('p', null, '여기에 제공하는 서비스 내용을 작성하세요.')
			),
			createElement(
				'section',
				{id: 'section3'},
				createElement('h2', null, '연락처'),
				createElement('p', null, '여기에 연락처 정보를 작성하세요.')
			)
		),
		createElement(
			'footer',
			null,
			createElement('p', null, '&copy; 2024 내 웹사이트. 모든 권리 보유.')
		)
	);
};
export default App;
```

## QUESTION createElement와 JSX의 차이가 어떤게 있을까요?

가독성과 불편함 때문에 JSX가 한다. 또한 createElement는 JS 문법이기 때문에 JSX가 컴파일 되는 환경이 아니더라도 React의 기능을 확인해 볼 수 있다.
(부가설명 첨부 필요)
