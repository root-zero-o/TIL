# Map 객체
## 1. Map 객체란?
- ES6에서 처음 등장한 새로운 데이터 구조
- 간단한 키와 값을 서로 연결(매핑)시켜 저장하며, 저장된 순서대로 각 요소들을 반복적으로 접근할 수 있도록 함
## 2. Object와 Map 비교
- Object의 키는 문자열이지만, Map의 키는 모든 값을 가질 수 있음
- Object는 크기를 수동으로 추적해야하지만, Map은 크기를 쉽게 얻을 수 있음
- Map은 삽입된 순서대로 반복함
- Map은 object와 달리 메소드만을 이용해 값을 넣고 뺌(object의 메소드가 제한적인 것과 달리, Map객체는 풍부한 메소드 제공)
> 👉 실행 시까지 키를 알 수 없고, 모든 키가 동일한 type이며 모든 값들이 동일한 type일 경우 Map 사용<br>
> 👉 각 개별 요소에 대해 적용해야 하는 로직이 있을 경우에는 object 사용

## 3. Map 객체의 메소드
```javascript
let max = new Map();

// set으로 맵 객체에 삽입
max.set("id", 0);
max.set("이름", "근영");
max.set("취미", "코딩");
max.set("나이", 25);

// 이차원 배열로 넘겨주는 것도 가능합니다
let michael = new Map([
    ["id", 0],
    ["이름", "근영"],
    ["취미", "코딩"],
    ["나이", 25]
])

// get으로 맵 객체 조회
max.get("이름"); // "근영"

// delete로 삭제
max.delete("나이"); // 삭제가 성공하면 true를 반환

// clear로 맵 안의 프로퍼티 전부삭제
max.clear();
```


## 참고
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Keyed_collections
- https://maxkim-j.github.io/posts/js-map
