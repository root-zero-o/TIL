# Customizing 💅

## Custom theme
- 색상, 스크린크기 등을 ```tailwind.config.js```에서 커스터마이징할 수 있다.
```javascript
// tailwind.config.js

module.exports = {
  purge: ["./pages/**/*.{js,ts,jsx,tsx}", "./components/**/*.{js,ts,jsx,tsx}"],
  theme: {
    screens: {
      "mobile" : {"min" : "320px", "max" : "480px"},
      "tablet" : {"min" : "768px", "max" : "1024px"},
      "desktop" : {"min" : "1024px"}  // 반응형 페이지 만들때 스크린 크기
    },
    colors: {
      ivory: "#FCF8E8",
      green: "#94B49F",
      orange: "#ECB390",
      red: "#DF7861",
      white: "#FFFFFF"  // 사용하고 싶은 색상
                        // 색상 추가 시 default 색상이 사라짐
                        // 따라서 사용할 색상을 모두 적어주어야 한다.
    },
    fontFamily: {
      sans: ['Graphik', 'sans-serif'],
      serif: ['Merriweather', 'serif'],  // 폰트 커스터마이징
    },
    extend: {
      spacing: {
        '128': '32rem',
        '144': '36rem',
      },
      borderRadius: {
        '4xl': '2rem',
      }
    },
  },
  plugins: [],
};
```

## layer
- CSS 파일에 ```@layer```을 추가해 반복을 줄일 수 있다.
- 아래와 같은 형식으로 사용(```@apply```사용)
```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  h1 {
    @apply font-serif font-semibold text-3xl text-white mb-2;
  }
  h2 {
    @apply font-serif font-medium text-lg text-white;
  }
}

@layer components {
  .container {
    @apply bg-ivory bg-green rounded-xl py-5 px-10 grid text-center space-y-2 shadow-xl;
  }
  .main-input {
    @apply font-serif w-64 border-4 border-orange rounded-xl my-5 p-2 focus:outline-none focus:border-red placeholder:italic;
  }
  .btn1 {
    @apply bg-red border-2 border-red py-2 px-5 ml-4 rounded-lg hover:border-2 hover:shadow-md;
  }
  .card {
    @apply bg-orange rounded-lg mt-5 py-5 px-10 flex justify-between items-center shadow-lg;
  }
  .checkbox {
    @apply w-5 h-5;
  }
}
```
- 해당 파일은 custom App에 import 해야 함
- 사용
```javascript
// pages/todoList.tsx

const TodoList = () => {


  return (
    <div className="container">  // component로 지정한 것들은 클래스를 주면 사용 가능
      <div className="flex flex-col mt-8">
        <h1>TO DO LIST</h1>
        <h2>with SSR  & React Query !</h2>
      </div>
      <Input/>
      <h2>Plans</h2>  // base로 지정한 것들은 클래스를 주지 않고 태그만 사용해도 적용됨
      <ListContainer/>
    </div>
  )
}

```

## 참고
- https://tailwindcss.com/docs/adding-custom-styles



