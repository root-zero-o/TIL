## Static 파일 적용하기

static 폴더 안의 JS, CSS 파일 적용하기

 ```url_for('폴더이름',filename='파일이름')```

```html
<link href="{{ url_for('static', filename='style.css') }}" rel="stylesheet">

<script src="{{ url_for('static', filename='script.js') }}" > </script>

<script src="{{ url_for('static', filename='js/script.js') }}" > </script>
```

#### 참고사이트
- https://infinitt.tistory.com/119
