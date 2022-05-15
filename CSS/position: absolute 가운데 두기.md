# ```position: absolute``` 가운데 두기

## 1. ```top```,```left```위치를 50%로 고정하기
```css
.title_content {
    position: absolute;
    top: 50%;
    left: 50%;
}
```
전체의 가운데를 기준으로 생성됨

## 2. ```transform```으로 요소의 사이즈만큼 반대로 이동시키기
```css
.title_content {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```
개체의 넓이와 높이만큼 50% 반대로 이동하는 원리

## 참고
- https://myhappyman.tistory.com/163
