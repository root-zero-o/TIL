# 다크모드 만들기 🌙

- 다크모드일때의 색 지정해주기 : 앞에 ```dark:```만 붙여주면 됨!
```css
styles/element.css

@layer components {
  .container {
    @apply bg-green dark:bg-dark rounded-xl w-2/3 py-5 px-10 grid text-center space-y-2 shadow-xl;
  }
```
- 다크모드 ```class```로 사용한다고 지정해주기
```javascript
// pages/tailwind.config.js

module.exports = {
  purge: ["./pages/**/*.{js,ts,jsx,tsx}", "./components/**/*.{js,ts,jsx,tsx}"],
  darkMode: "class",  // 요렇게 지정해준다.
  theme: {
    screens: {
      "mobile" : {"min" : "320px", "max" : "480px"},
      "tablet" : {"min" : "768px", "max" : "1024px"},
      "desktop" : {"min" : "1024px"}
    },
    colors: {
      ivory: "#FCF8E8",
      green: "#94B49F",
      orange: "#ECB390",
      red: "#DF7861",
      white: "#FFFFFF",
      black:"#000000",  // 다크모드에서 사용할 색도 지정해주기
      dark:"#413F42",
      grey: "#7F8487"
    },
    extend: {},
  },
  plugins: [],
};
```
- HTML에 class 지정해주기
```javascript
//pages/_document.tsx

import Document, { Html, Head, Main, NextScript } from 'next/document'
// import 해준 뒤 아래 구성으로 작성해야 한다.

class MyDocument extends Document {

  render() {
    return (
      <Html className='dark'>  // Html에 class 지정해주기
        <Head>
            <title>Todo List</title>
            <meta charSet='utf-8'></meta>
        </Head>
        <body>
          <Main />
          <NextScript />
        </body>
      </Html>
    )
  }
}

export default MyDocument
```
- 버튼을 누르면 class가 바뀌게 설정해주기
```javascript
// components/DarkMode.tsx

import React from 'react'

const DarkMode = () => {

    // light 버튼 눌렀을 때
    const onLightMode = () => {
        document.documentElement.classList.remove("dark") 
    }

    // dark 버튼 눌렀을 때
    const onDarkMode = () => {
        document.documentElement.classList.add("dark")
    }

  return (
    <div className="absolute top-10 right-10">
        <button onClick={onLightMode}className="bg-green font-serif p-4 rounded-lg mr-5 text-white">light</button>
        <button onClick={onDarkMode} className="bg-green font-serif p-4 rounded-lg text-white">dark</button>
    </div>
  )
}

export default DarkMode;
```

## 참고
- https://tailwindcss.com/docs/dark-mode
