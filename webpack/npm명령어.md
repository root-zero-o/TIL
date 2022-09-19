# NPM 명령어 정리

- node.js 버전 확인
```
node -v  
```

- package.json 생성
```
npm init
npm init -y  // 기본값으로 생성
```

- 라이브러리 설치(dependencies)
    - 배포용 라이브러리 : 애플리케이션 로직을 구현하는 것과 연관이 있다.
    - ```npm run build```로 빌드하면 최종 애플리케이션 코드 안에 포함된다.
    - react, angular, chart, vue 등
```
npm install (라이브러리 이름)
npm install jquery  // jquery 설치
npm install gulp --global  // gulp 전역설치(시스템 레벨에서 사용할 라이브러리 설치)
```

- 라이브러리 설치(devDependencies)
     - 개발용 라이브러리(개발 보조 라이브러리)
     - 빌드하고 배포할 때 애플리케이션 코드에서 빠진다.
     - webpack, js-compression, sass 등
      
```
npm install vue --save-dev
npm i vue -D
```

- 라이브러리 삭제
```
npm uninstall (라이브러리 이름)
npm uninstall gulp  // gulp 삭제
```

## 참고
- 인프런 '프론트엔드 개발자를 위한 웹팩'
