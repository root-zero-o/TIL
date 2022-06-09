# Git 명령어 - commit
- 버전을 만들 때 이용하는 명령어
- stage area에 있는 변경사항을 git repository에 옮겨줌

## basic
```
git commit
```
- 아무 옵션 없이 입력했을 때는 기본 template이 뜸
```
Title // 여기에 commit message Title 작성

Description  // 여기에 commit message Description 작성

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch master
#
# Initial commit
#
# Changes to be committed:
#	new file:   b.txt
#	new file:   style.css
#
# Untracked files:
#	.gitignore
#	d.txt
#             // 다하고 저장한 뒤 창 닫기
```
```
git log  // 기록 보기
```

## 간단하게 commit
#### 입력
```
git commit -m "second commit"  // commit message 바로 입력
```
#### 결과
```
[master (root-commit) ad8c512] second commit
 4 files changed, 6 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 b.txt
 create mode 100644 d.txt
 create mode 100644 style.css
```
```
commit ad8c512494d75985a8644970a6221e0fe77821cb (HEAD -> master)   // git log 입력 시 결과
Author: RootZero <rootzero17@gmail.com>
Date:   Fri Jun 10 01:46:17 2022 +0900

    second commit
```

## 한번에 commit
```
git commit -am  // -a : working directory와 staging area에 있는 것 전부다 
                // m : 메시지와 함께
```

## commit message Tips
```
Initialise project
Add LoginService module
Add UserRepository module
Add Welcome page
Add About page
Add light theme
```
- 현재형으로, 동사로 만들기
- commit message에 맞게 해당하는 내용만 포함할 것
