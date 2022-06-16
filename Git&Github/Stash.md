# Git 명령어 - Stash

## 1. git stash ?
- 아직 마무리하지 않은 작업을 스택에 잠시 저장할 수 있도록 하는 명령어
- 아직 완료하지 않은 일을 commit하지 않고 나중에 다시 꺼내 마무리 할 수 있음 !
- stash : 아래에 해당하는 파일들을 보관해두는 장소
    - Modified 이면서 Tracked 상태인 파일 : tracked 상태인 파일을 수정한 경우
    - Staging Area에 있는 파일 : git add 명령을 실행한 경우
    
## 2. 사용법
- 새로운 stash 만들기 (다른 브랜치로 변경 가능)
```
git stash 
git stash save
```
- stash 목록 확인
```
git stash list
```
- stash 적용하기(했던 작업 다시 가져오기)
```
git stash apply   // 가장 최근의 stash를 가져와 적용
git stash apply [stash 이름]  // [stash 이름]에 해당하는 stash를 적용함
git stash apply --index  // index 옵션을 주어야 staged 상태까지 복원
```
*apply를 해도 해당 stash는 스택에 남아있음*

- stash 제거
```
git stash drop  // 가장 최근의 stash 제거
git stash drop [stash 이름]  // [stash 이름]에 해당하는 stash를 제거함
git stash pop  // 적용과 동시에 스택에서 해당 stash 제거
```
- stash 되돌리기 (실수로 잘못 stash 적용한 것 되돌리기)
```
git stash show -p | git apply -R   // 가장 최근의 stash를 사용해 패치를 만들고 그것을 거꾸로 적용
git stash show -p [stash 이름] | git apply -R
```

## 참고
- https://gmlwjd9405.github.io/2018/05/18/git-stash.html
