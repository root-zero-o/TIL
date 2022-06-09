# Git 명령어 - Basic👆

## 1. 기본 구조
```git
git [명령어] [옵션]
```
- 명령어 확인 : [Git 공식문서](https://git-scm.com/docs)

<br>

## 2. 터미널 명령어
#### 📁파일로 이동
```
cd [파일이름]
```
#### 📁디렉토리 만들기
```
mkdir [프로젝트 이름]  // '프로젝트 이름'이라는 디렉토리 만들기
```
#### 📁디렉토리 확인
```
ls -a, ls -al  // 디렉토리 안의 모든 파일과 디렉토리를 보여줌
ls -l  // 파일에 대한 정보를 보여줌(사용권한, 소유자, 그룹, 크기, 날짜 등)
ls --help  // ls 명령어에 대한 도움말 출력
```
#### 📁파일 만들기
```
echo [내용] > [파일]  // [파일]에 [내용]을 적어 생성
echo hello world! > a.txt  // a라는 텍스트 파일에 hello world!를 적어 생성
```

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

