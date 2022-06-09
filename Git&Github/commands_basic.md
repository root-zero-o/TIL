# Git 명령어 - Basic👆

## 1. 기본 구조
```git
git [명령어] [옵션]
```
- 명령어 확인 : [Git 공식문서](https://git-scm.com/docs)

<br>

## 2. 터미널 명령어
#### 📁작업위치
- ```pwd``` : 현재 작업 위치 알려줌(Print working directory)
- ```ls``` : 현재의 directory의 모든 파일들을 보여줌(list files)
- ```cd..``` : 상위 디렉토리로 이동 (change directory)
- ```cd~``` : 사용자의 홈디렉토리로 이동
- ``` cd 디렉토리명``` : 원하는 디렉토리로 이동(단계적으로 이동)
#### 📁디렉토리 만들기
- ```mkdir 디렉토리명```  :  새로운 디렉토리 생성(make directory)
- ```rm -rf 디렉토리명``` : 디렉토리 삭제. 디렉토리와 디렉토리 하위 모든 파일 삭제
- ```cp -R <sourcedir> <destdir>``` : 디렉토리 복사(sourcedir : 카피하고 싶은 폴더, destdir : 옮기고 싶은 폴더명)
#### 📁디렉토리 확인

- ```cat 파일명``` : 파일의 contents를 보여줌
- ```touch .파일명``` : 파일 만들기
- ```echo "파일내용" > 파일명``` : 내용과 함께 새로운 파일 만들기
- ```ls -a, ls -al``` : 디렉토리 안의 모든 파일과 디렉토리를 보여줌
- ```ls -al | grep .파일명``` : 특정 파일 불러오기. 찾고 싶은 파일이 있을 때
- ```ls -l```  : 파일에 대한 정보를 보여줌(사용권한, 소유자, 그룹, 크기, 날짜 등)
- ```ls --help```:  ls 명령어에 대한 도움말 출력
#### 📁기타
- ```ctrl + L ``` : 터미널 화면 clear

<br>

## 3. git 초기화
#### 📁초기화 및 삭제
```
git init  // git 초기화, master 브랜치가 생성됨
rm -rf .git  // git 파일 삭제
```
#### 📁명령어 줄이기
```
git config --global alias.[줄임말] [줄이고싶은 명령어]  // 명령어 줄이기
git config --global alias.st status  // status 명령어를 st로 줄임
```
#### 📁명령어 옵션 살펴보기
```
git [명령어] --h  // 해당 명령어의 옵션 살펴보기
```
#### 📁git 상태 보기
```
git status
```
```
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        a.txt
        b.txt
        c.txt   // tracking 되지 않은 파일이 이렇게 있어

nothing added to commit but untracked files present (use "git add" to track)  // git add를 이용해 track 해 !
```

## 참고
- [드림코딩 유튜브](https://www.youtube.com/watch?v=Z9dvM7qgN9s)
- https://velog.io/@grinding_hannah/Git-Git-%EC%82%AC%EC%9A%A9%EB%B2%95-%EB%B0%8F-%ED%84%B0%EB%AF%B8%EB%84%90-%EB%AA%85%EB%A0%B9%EC%96%B4-%EC%A0%95%EB%A6%AC
