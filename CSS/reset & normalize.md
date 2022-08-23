# Reset & Normalize

- 브라우저에서는 가장 먼저 ```User-agent Stylesheet```가 적용된다.(브라우저에서 제공하는 기본 스타일)
- 따라서 똑같은 button 이라도 크롬, 사파리, 엣지 등 브라우저마다 다른 스타일이 적용된다.
- 이 문제를 해결하기 위해 ```사전 정의한 스타일시트```를 통해 기본 스타일을 ```무효화```시킨다.

## reset
- 모든 브라우저 스타일을 ```초기화```한다.
- 디폴트 색 등이 모두 사라지기 때문에, 원래 스타일이 헷갈릴 수 있다..
- Styled-Components 에서는 ```styled-reset```을 사용하면 된다.

## normalize
- 브라우저 스타일을 여러 브라우저에서 ```동일해 보이도록``` 한다.
- 정규화가 필요한 스타일만 normalize할 수 있다. 
- Styled-Components 에서는 ```styled-normalize```를 사용하면 된다.

## 참고
- https://nykim.work/100
