# setting

- 설치하기
```
 yarn add @apollo/client qraphql
```

- client 생성하기
```javascript
// client.tsx

import { ApolloClient, gql, InMemoryCache } from "@apollo/client";

const client = new ApolloClient({
  uri: "http://localhost:4000/",
  cache: new InMemoryCache(),
});

client
  .query({
    query: gql`  // 여기에 쿼리가 들어감
      {
        allMovies {
          title
        }
      }
    `,
  })
  .then((data) => console.log(data));

export default client;
```

- _app.tsx에서 감싸주기
```javascript
// _app.tsx

import type { AppProps } from "next/app";
import { ApolloProvider } from "@apollo/client";  // import 해주기
import client from "./client";
import "../styles/globals.css";

const App = ({ Component, pageProps }: AppProps) => {
  return;
  <ApolloProvider client={client}>  // 감싸주고 client를 준다.
    <Component {...pageProps} />
  </ApolloProvider>;
};

export default App;

```
