# Git 명령어 - Fetch

## 1. git fetch ?
- 원격저장소에 있는 변경사항들을 로컬에 가져오기 전에 변경사항을 확인하고 싶은 경우에 사용하는 명령어
- 원격저장소에서 파일을 병합하기 전에 병합할지 말지 확인
- 최신 커밋 이력은 이름없는 브랜치로 로컬에 가져옴("FETCH_HEAD"의 이름으로 체크아웃 가능)
- git pull = git fetch + git merge

## 2. 사용
- fetch 실행
```
git fetch
git checkout FETCH_HEAD  // 받아온 커밋 살펴보기
```
- 커밋 합치기
```
git checkout master  // master 브랜치로 이동
git merge FETCH_HEAD  // 파일 병합
```

*직접 사용해보고 더 정리할 것*
