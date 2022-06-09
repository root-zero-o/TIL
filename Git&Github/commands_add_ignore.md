# Git 명령어 - add, ignore

## 1. git add

#### 📁git add
```
git add [파일명]  // [파일]을 staging area로 add 한다!
git add *.txt   // txt로 끝나는 모든 파일을 add 한다
```
```
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   a.txt
        new file:   b.txt
        new file:   c.txt    // commit할 준비가 되었다!
```
*🤷여기서 파일이 수정된다면?*
```
No commits yet                                                          
                                                                        
Changes to be committed:                                                
  (use "git rm --cached <file>..." to unstage)                          
        new file:   a.txt                                               
        new file:   b.txt                                               
        new file:   c.txt         // a, b, c는 staging area에 있음                 
                                                                        
Changes not staged for commit:                                          
  (use "git add <file>..." to update what will be committed)            
  (use "git restore <file>..." to discard changes in working directory) 
        modified:   a.txt         // modified 상태의 a는 tracking되고 있으나, staging area에 있는 것은 아님                     
```
#### 📁staging area에서 내리기
```
git rm --cached [파일명]
```

----


## 2. git ignore
- 📁 gitignore 파일에 추가
```
echo [파일명] > .gitignore
echo *.log > .gitignore  // 모든 log 파일을 gitignore에 추가
echo build/ > .gitignore  // 특정 디렉토리(build) 안에 있는 파일들 추가
echo build/*.log > .gitignore  // 특정 디렉토리(build) 안에 있는 log 추가
```
```
No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   b.txt
        new file:   style.css

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore  // log파일은 .gitignore에 들어감
```
## 참고
- [드림코딩 유튜브](https://www.youtube.com/watch?v=Z9dvM7qgN9s)
