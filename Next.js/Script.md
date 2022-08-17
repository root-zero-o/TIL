# Script
  
## 🤔 왜 써요?
- ```Next.js```에서 지원하는 ```<Script>```는 HTML ```<script>```의 extension이다.

- 애플리케이션 안에서(아무곳에서나) third-party script의 우선순위를 매겨 로딩할 수 있게 해준다 !
- 그래서 performance를 개선하는 데에 매우 좋다.
  
## 🤔 어떻게 써요?
### import 해주기

```javascript
import Script from 'next/script'
```

### 컴포넌트 안에서 사용해주기
```javascript
return (
    <>
      <Script
        src={`https://dapi.kakao.com/v2/maps/sdk.js?appkey=${NEXT_PUBLIC_KAKAOMAP_KEY}&autoload=false`}
        onLoad={() => window.kakao.maps.load(initMap)}
      />
      <div
        ref={containerRef}
        className="w-full h-[300px] desktop:h-[400px] absolute top-20"
      ></div>
    </>
  );
```

### 프로퍼티
- ```beforeInteractive```
    - 서버에서 실행된다.
    
    - self-bundled Javascript가 실행되기 전에 실행된다.
    - 페이지가 interactive 해지기 전에 fetch되고 실행되어야 하는 중요한 스크립트에 사용해야 한다.
    - ```_document.js```에서만 실행된다.
```javascript
import { Html, Head, Main, NextScript } from 'next/document'
import Script from 'next/script'

export default function Document() {
  return (
    <Html>
      <Head />
      <body>
        <Main />
        <NextScript />
        <Script
          src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.20/lodash.min.js"
          strategy="beforeInteractive"
        ></Script>
      </body>
    </Html>
  )
```

- ```afterInteractive```
    - default이다.
    - 클라이언트에서 Next.js가 페이지를 hydrate한 뒤에 실행된다.
    - 급하게 실행하지 않아도 되고, 페이지가 interactive해지자마자 실행되어야 하는 스크립트에 사용한다.

- ```lazyOnload```
    - 모든 리소스가 fetch된 뒤인 idle time에 실행된다.
    - background나 우선순위가 낮은 스크립트에 사용한다.

- Inline Scripts
    - ```Script``` 컴포넌트 안에서 script를 사용할 수도 있다.
```javascript
<Script id="show-banner" strategy="lazyOnload">
  {`document.getElementById('banner').classList.remove('hidden')`}
</Script>

// dangerouslySetInnerHTML 사용하는 방법
<Script
  id="show-banner"  // id는 필수적으로 적어주어야 한다.
  strategy="lazyOnload"
  dangerouslySetInnerHTML={{
    __html: `document.getElementById('banner').classList.remove('hidden')`,
  }}
/>
```

- ```onLoad```
    - ```beforeInteractive```와 사용할 수 없다.(사용하려면 ```onReady```를 사용해야 한다.)
    - 로딩이 끝난 후 한 번만 자바스크립트 코드를 실행하고 싶을 때 사용한다.
```javascript
return (
    <>
      <Script
        src={`https://dapi.kakao.com/v2/maps/sdk.js?appkey=${NEXT_PUBLIC_KAKAOMAP_KEY}&autoload=false`}
        onLoad={() => window.kakao.maps.load(initMap)}
      />
      <div
        ref={containerRef}
        className="w-full h-[300px] desktop:h-[400px] absolute top-20"
      ></div>
    </>
  );
```

- ```onReady```
    - 로딩이 끝난 후, 컴포넌트가 mount될 때 마다 실행하고 싶을 때 사용한다.
```
import { useRef } from 'react'
import Script from 'next/script'

export default function Home() {
  const mapRef = useRef()
  return (
    <>
      <div ref={mapRef}></div>
      <Script
        id="google-maps"
        src="https://maps.googleapis.com/maps/api/js"
        onReady={() => {
          new google.maps.Map(mapRef.current, {
            center: { lat: -34.397, lng: 150.644 },
            zoom: 8,
          })
        }}
      />
    </>
  )
}
```

- ```onError```
    - 에러 핸들링할 때 사용한다.
    - ```beforeInteractive```와 사용할 수 없다.
```javascript
import Script from 'next/script'

export default function Home() {
  return (
    <>
      <Script
        id="will-fail"
        src="https://example.com/non-existant-script.js"
        onError={(e) => {
          console.error('Script failed to load', e)
        }}
      />
    </>
  )
}
```

## 참고
- https://nextjs.org/docs/basic-features/script
