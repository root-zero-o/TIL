# Customizing π

## Custom theme
- μμ, μ€ν¬λ¦°ν¬κΈ° λ±μ ```tailwind.config.js```μμ μ»€μ€ν°λ§μ΄μ§ν  μ μλ€.
```javascript
// tailwind.config.js

module.exports = {
  purge: ["./pages/**/*.{js,ts,jsx,tsx}", "./components/**/*.{js,ts,jsx,tsx}"],
  theme: {
    screens: {
      "mobile" : {"min" : "320px", "max" : "480px"},
      "tablet" : {"min" : "768px", "max" : "1024px"},
      "desktop" : {"min" : "1024px"}  // λ°μν νμ΄μ§ λ§λ€λ μ€ν¬λ¦° ν¬κΈ°
    },
    colors: {
      ivory: "#FCF8E8",
      green: "#94B49F",
      orange: "#ECB390",
      red: "#DF7861",
      white: "#FFFFFF"  // μ¬μ©νκ³  μΆμ μμ
                        // μμ μΆκ° μ default μμμ΄ μ¬λΌμ§
                        // λ°λΌμ μ¬μ©ν  μμμ λͺ¨λ μ μ΄μ£Όμ΄μΌ νλ€.
    },
    fontFamily: {
      sans: ['Graphik', 'sans-serif'],
      serif: ['Merriweather', 'serif'],  // ν°νΈ μ»€μ€ν°λ§μ΄μ§
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
- CSS νμΌμ ```@layer```μ μΆκ°ν΄ λ°λ³΅μ μ€μΌ μ μλ€.
- μλμ κ°μ νμμΌλ‘ μ¬μ©(```@apply```μ¬μ©)
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
- ν΄λΉ νμΌμ custom Appμ import ν΄μΌ ν¨
- μ¬μ©
```javascript
// pages/todoList.tsx

const TodoList = () => {


  return (
    <div className="container">  // componentλ‘ μ§μ ν κ²λ€μ ν΄λμ€λ₯Ό μ£Όλ©΄ μ¬μ© κ°λ₯
      <div className="flex flex-col mt-8">
        <h1>TO DO LIST</h1>
        <h2>with SSR  & React Query !</h2>
      </div>
      <Input/>
      <h2>Plans</h2>  // baseλ‘ μ§μ ν κ²λ€μ ν΄λμ€λ₯Ό μ£Όμ§ μκ³  νκ·Έλ§ μ¬μ©ν΄λ μ μ©λ¨
      <ListContainer/>
    </div>
  )
}

```

## μ°Έκ³ 
- https://tailwindcss.com/docs/adding-custom-styles



