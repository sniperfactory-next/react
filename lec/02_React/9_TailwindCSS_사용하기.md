# Tailwind CSS 사용하기

## 설치하기

```sh
npm install -D tailwindcss
npx tailwindcss init
```

## tailwind.config.js 파일 수정하기

```js
module.exports = {
	content: ['./src/**/*.{html,js}'],
	theme: {
		extend: {},
	},
	plugins: [],
};
```

## src/assets/globals.css 파일 수정하기

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## vite.config.ts 수정하기

```js
import {defineConfig} from 'vite';
import react from '@vitejs/plugin-react-swc';
import tailwindcss from 'tailwindcss';

// https://vitejs.dev/config/
export default defineConfig({
	plugins: [react()],
	css: {
		postcss: {
			plugins: [tailwindcss()],
		},
	},
});
```
