# Pixel 프리셋 설정하기

- 배열의 ```index```를 사용해주기
```javascript
// tailwind.config.js
const px0_10 = { ...Array.from(Array(11)).map((_, i) => `${i}px`) };  // length가 11인 배열 만들어서 index 사용
const px0_100 = { ...Array.from(Array(101)).map((_, i) => `${i}px`) };
const px0_200 = { ...Array.from(Array(201)).map((_, i) => `${i}px`) };

module.exports = {
  theme: {
    extend: {
      borderWidth: px0_10,
      fontSize: px0_100,
      lineHeight: px0_100,
      minWidth: px0_200,
      minHeight: px0_200,
      spacing: px0_200,
      ...
    }
  }
}
```

- 사용
```javascript
<div className="p-8 h-35 text-12 border-2 rounded-5">
```

*진짜 멋진 방법이다 ..*

## 참고
- https://fe-developers.kakaoent.com/2022/220303-tailwind-tips/
