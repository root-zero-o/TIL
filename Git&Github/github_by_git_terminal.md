# Git terminal로 Github 사용하기😉

## 👉 처음 업로드할 때
#### 초기화 
```
git init
```
#### 추가할 파일 더하기 
```
git add .
```
#### 상태 확인 
```
git status
```
#### 히스토리 만들기 
```
git commit -m "히스토리 이름"
```
#### Github repository에 연결
```
git remote add origin 깃헙 repo 주소
```
#### 잘 연결됐는지 확인
```
git remote -v  // 연결한 주소값이 잘 뜨면 성공
```
#### Github로 올리기
```
git push origin master  // master 자리에는 branch 이름이 들어가면 됨
```

## 👉 Github에 업데이트
#### 추가할 파일 더하기
```
git add .
```
#### 히스토리 만들기
```
git commit -m "first commit"
```
#### Github로 올리기
```
git push origin master  // master 자리에는 branch 이름이 들어가면 됨
```

## 👉 팀프로젝트 하기
#### Github에서 소스코드 다운로드
```
git clone 주소 폴더이름
```
- 주소는 깃허브에서 들고와야 함
- 폴더이름은 선택사항!
    - 폴더이름을 줄 경우 : 그 폴더가 새로 생성되면서 코드 다운로드됨
    - 폴더이름을 안줄 경우 : 깃허브 프로젝트 이름으로 폴더가 자동으로 생기고 그 안에 코드 다운로드됨 

#### Github에서 내 브랜치 만들기
```
git checkout -b 브랜치이름
```
#### 내 브랜치에 소스코드 업데이트
```
git add .
git commit -m "first commit"
git push origin 브랜치이름
```
#### 마스터 브랜치에 소스 가져오기(pull)
```
git pull origin master  // pull 하기 전에는 기존 소스코드들을 commit 먼저 해야함!
```
#### 브랜치끼리 이동하는 법
```
git checkout 브랜치이름
```

## 참고
- https://hackmd.io/@oW_dDxdsRoSpl0M64Tfg2g/ByfwpNJ-K
