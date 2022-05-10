## url_for 함수

### 1. url_for 함수  

Flask의 url_for 함수는 주어진 뷰의 실제 URL을 반환함
```url_for('babo', name='geunyeong')```을 호출하면 'babo' URL에서 name의 값이 'geunyeong'이 되는 url 주소를 반환함 
- 실행 문맥에 따라 URL이 달라지는 경우 유용

### 2. static 폴더 안의 JS, CSS 파일 적용하기  

 ```url_for('폴더이름',filename='파일이름')```

```html
<link href="{{ url_for('static', filename='style.css') }}" rel="stylesheet">

<script src="{{ url_for('static', filename='script.js') }}" > </script>

<script src="{{ url_for('static', filename='js/script.js') }}" > </script>
```

#### 참고사이트
- https://infinitt.tistory.com/119
- https://kimjingo.tistory.com/95
- https://newbie-developer.tistory.com/70
