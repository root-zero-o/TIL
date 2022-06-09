# Git Settings🛠

## 1. Initial Settings

**설정 확인**
```
git config --list 
```
**설정 확인(file)**
```
git config --global -e
```
**VSCode로 열기**
```
git config --global core.editor "code" // VSCode가 열리면서 동시에 다른 명령어 실행할 수 있도록 터미널 활성화 됨
git config --global core.editor "code --wait" // 열린 VSCode가 종료되기 이전에 다른 명령어 수행X
git config --global -e // VSCode 열기
```

## 2. 사용자 정보 설정
```
git config --global user.name "이름"  // 사용자 이름 설정
git config --global user.email "이메일주소"  // 사용자 이메일 설정
git config user.name // 이름 확인
git config user.email // 이메일 확인
```
```
git config --global core.autocrlf true // Mac은 true 대신 input 
```
- 운영체제마다 줄바꿈 방식이 달라 문제가 생길 수 있음
- 이를 운영체제마다 깃에서 수정해서 저장 및 불러오기 해줌!

## 참고
- [드림코딩 유튜브](https://www.youtube.com/watch?v=Z9dvM7qgN9s)
