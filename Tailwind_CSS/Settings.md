# Settings

### 설치
```
yarn add -D tailwindcss postcss autoprefixer
```
- ```postcss```가 빌드 시에 tailwind CSS를 일반 CSS로 변환해준다.

### 설정파일
```
yarn tailwind css init  // tailwind.config.js 파일이 최상단에 생성된다.
```

```typescript
// postcss.config.js

module.exports = {
  plugins: {
    tailwindcss: { config: './tailwind.config.js' },
    autoprefixer: {},
  },
};
```
```typescript
// tailwind.config.js

module.exports = {
  content: ['./src/**/*.tsx', './public/index.html'],
  theme: {
    extend: {},
  },
  plugins: [],
};
```
- 리액트 파일들과 ```index.html```을 포함시켜준다.

### 글로벌 CSS 설정
```css
// src/tailwind.css

@tailwind base;
@tailwind components;
@tailwind utilities;
```
- ```@tailwind```부분 빨간줄 뜨면 vscode의 postcss 익스텐션 사용하기

### import
```typescript
// src/index.tsx

import React from 'react';
import { render } from 'react-dom';
import App from './App';
import './tailwind.css';

render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root'),
);
```

## 참고
- https://dev.classmethod.jp/articles/add-tailwindcss-in-react/#toc-8
- https://tailwindcss.com/docs/installation
