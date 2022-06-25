# Next.js에서 style 주기

## 1. modules
- ```[name].module.css``` 라는 css 모듈 파일을 만듦
- 자동으로 class 이름을 랜덤한 문자열로 바꿔주기 때문에, 다른 파일과 같은 class 이름을 사용해도 충돌하지 않음

components/Button.module.css
```css
.error {
  color: white;
  background-color: red;
}
```

components/Button.js
```javascript
import styles from './Button.module.css'

export function Button() {
  return (
    <button
      type="button"
      // Note how the "error" class is accessed as a property on the imported
      // `styles` object.
      className={styles.error}
    >
      Destroy
    </button>
  )
}
```

## style jsx
```javascript
function HelloWorld() {
  return (
    <div>
      Hello world
      <p>scoped!</p>
      <style jsx>{`
        p {
          color: blue;
        }
        div {
          background: red;
        }
        @media (max-width: 600px) {
          div {
            background: blue;
          }
        }
      `}</style>
      <style global jsx>{`
        body {
          background: black;
        }
      `}</style>
    </div>
  )
}

export default HelloWorld
```

## 참고
- https://nextjs.org/docs/basic-features/built-in-css-support#adding-a-global-stylesheet
- 노마드코더 'Next.js 시작하기'

