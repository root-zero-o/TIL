# Next.js + Styled-Components 세팅

1. styles/global-style.ts
```typescript
import { createGlobalStyle } from "styled-components";  // 1. globalStyle 가져오기
import { normalize } from "styled-normalize";  // 2. CSS normalize 하기

// 3. GlobalStyle 만들어주기
export const GlobalStyle = createGlobalStyle`  
    ${normalize}
    a {cursor:pointer; text-decoration:none;}
    *{
        margin: 0;
        padding: 0;
        outline:0;
        box-sizing:border-box;
        font-family: "SpoqaHanSansNeo-Regular"; 
    }
`;
```

2. styles/styled.d.ts
```typescript
import "styled-components";

// DefaultTheme 에서 사용해 줄 것 타입 지정하기
declare module "styled-components" {
  export interface DefaultTheme {
    colors: {
      black: string;
      white: string;
      gray: string;
      deepPurple: string;
    };
  }
}
```

3. styles/theme.ts
```typescript
// 지정한 타입을 불러와 사용해준다.
import { DefaultTheme } from "styled-components";

export const theme: DefaultTheme = {
  colors: {
    black: "#000000",
    white: "#ffffff",
    gray: "#CCCCCC",
    deepPurple: "#6A30F9",
  },
};
```

4. pages/_app.tsx

```typescript
import "../styles/globals.css";
import type { AppProps } from "next/app";
import { ThemeProvider } from "styled-components";
import { GlobalStyle } from "../styles/global-style";
import { theme } from "../styles/theme";

function MyApp({ Component, pageProps }: AppProps) {
  return (
    <ThemeProvider theme={theme}>
      <GlobalStyle />
      <Component {...pageProps} />
    </ThemeProvider>
  );
}

export default MyApp;
```

5. typescript 사용해서 props 넘겨주기
```typescript
const StH2 = styled.h2<{ color: string }>`  // props의 타입을 정해준다.
  font-size: 40px;
  font-weight: 700;
  color: ${(props) => props.color};
  margin-bottom: 10px;
  @media (max-width: 720px) {
    font-size: 30px;
  }
`;
```
