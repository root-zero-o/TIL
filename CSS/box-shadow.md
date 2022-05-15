# box-shadow
- 테두리를 감싼 그림자 효과를 추가
- 수평거리(offset-x), 수직거리(offset-y) 흐릿함, 확산 정도, 색상을 나타낼 수 있음
- 값을 지정하지 않으면(기본값) 공중에 떠있는 것처럼 밖에 드리우는 그림자가 됨

```css
/* offset-x, offset-y, color */
box-shadow: 10px -10px tomato;

/* offset-x, offset-y, blur-radius, color */
box-shadow: 10px 5px 5px black;

/* offset-x, offset-y, blur-radius, spread-radius, color */
box-shadow: 2px 1px 1px 1px rgba(0,0,0,0.5);

/* inset | offset-x | offset-y | color */
box-shadow: inset 5em 1em gold;
```
- ```inset``` : 움푹 들어간 것처럼 그림자가 요소의 테두리 안, 배경색 위, 내부 콘텐츠 밑에 그려짐
- ```em``` : 요소의 글꼴 크기

## 참고
- https://developer.mozilla.org/ko/docs/Learn/CSS/Building_blocks/Values_and_units
- https://developer.mozilla.org/ko/docs/Web/CSS/box-shadow
