# Settings

- Next.js + TypeScript 설치
```
yarn create next-app --typescript
```

- tsconfig.json 생성
```
tsc --init
```

- tsconfig.json 설정
```typescript
{
  "compilerOptions": {
    "target": "es6",  // 컴파일된 코드가 어떤 환경에서 실행될지 정의
                      // 화살표 함수 사용 후 target을 es5로 하면 function 함수로 변환해줌
    "module": "commonjs",  // 컴파일된 코드가 어떤 모듈 시스템을 사용할지 정의함
    "strict": true,  // 모든 타입 체킹 옵션 활성화
    "esModuleInterop": true  // commonjs 모듈 형태로 이루어진 파일을 es2015 모듈 형태로 불러올 수 있게 해줌
    "outDir": "./dist"  // 컴파일된 파일들이 저장되는 경로 지정
  }
}
```
