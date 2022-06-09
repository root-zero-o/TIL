# Git terminal로 github 팀프로젝트 하기🤛

#### Github에서 소스코드 다운로드
```
git clone 주소 폴더이름
```
- 주소는 깃허브에서!
- 폴더이름은 선택사항
    - 폴더이름을 줄 경우 : 그 폴더가 새로 생성이 되면서 그 안에 코드들이 다운로드됨
    - 폴더이름을 안 줄 경우 : 깃허브 프로젝트 이름으로 폴더가 자동으로 생기고, 그 안에 코드가 다운로드됨

#### 브랜치 만들기
```
git checkout -b 브랜치이름
```
#### 내 브랜치에 소스코드 업데이트
```
git add .
git commit -m "커밋메시지"
git push origin 브랜치이름
```
#### 마스터 브랜치에 소스 가져오기(pull)
```
`git pull origin master
```
#### 브랜치 이동
```
git checkout 브랜치이름/커밋ID
```
- 브랜치가 생성될 시점의 그 모습 그대로 유지가 됨
- 작업할 때는 어느 브랜치의 워킹 디렉토리에서 작업했는지 반드시 기억해야함 !
- 🤷어느 브랜치에서 작업했는지 기억나지 않으면?
```
git log --graph --oneline --decorate --all
```


## 참고
- https://hackmd.io/@oW_dDxdsRoSpl0M64Tfg2g/ByfwpNJ-K
- https://velog.io/@grinding_hannah/Git-Git-%EC%82%AC%EC%9A%A9%EB%B2%95-%EB%B0%8F-%ED%84%B0%EB%AF%B8%EB%84%90-%EB%AA%85%EB%A0%B9%EC%96%B4-%EC%A0%95%EB%A6%AC
