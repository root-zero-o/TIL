# Git ๋ช๋ น์ด - add, ignore

## 1. git add

#### ๐git add
```
git add [ํ์ผ๋ช]  // [ํ์ผ]์ staging area๋ก add ํ๋ค!
git add *.txt   // txt๋ก ๋๋๋ ๋ชจ๋  ํ์ผ์ add ํ๋ค
```
```
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   a.txt
        new file:   b.txt
        new file:   c.txt    // commitํ  ์ค๋น๊ฐ ๋์๋ค!
```
*๐คท์ฌ๊ธฐ์ ํ์ผ์ด ์์ ๋๋ค๋ฉด?*
```
No commits yet                                                          
                                                                        
Changes to be committed:                                                
  (use "git rm --cached <file>..." to unstage)                          
        new file:   a.txt                                               
        new file:   b.txt                                               
        new file:   c.txt         // a, b, c๋ staging area์ ์์                 
                                                                        
Changes not staged for commit:                                          
  (use "git add <file>..." to update what will be committed)            
  (use "git restore <file>..." to discard changes in working directory) 
        modified:   a.txt         // modified ์ํ์ a๋ tracking๋๊ณ  ์์ผ๋, staging area์ ์๋ ๊ฒ์ ์๋                     
```
#### ๐staging area์์ ๋ด๋ฆฌ๊ธฐ
```
git rm --cached [ํ์ผ๋ช]  // staging area์ ์ถ๊ฐ๋ ํ์ผ์ ๋ค์ working directory๋ก ๋ด๋ ค๋ณด๋ด๋ ๋ช๋ น์ด
git rm -r -cached .  // ํ์ฌ staging directory์ ์๋ ๋ชจ๋  ํ์ผ์ ํ๊บผ๋ฒ์ ๋ค์ working directory๋ก ๋ด๋ฆฌ๊ธฐ
```

----


## 2. git ignore
- ๐ gitignore ํ์ผ์ ์ถ๊ฐ
```
echo [ํ์ผ๋ช] > .gitignore
echo *.log > .gitignore  // ๋ชจ๋  log ํ์ผ์ gitignore์ ์ถ๊ฐ
echo build/ > .gitignore  // ํน์  ๋๋ ํ ๋ฆฌ(build) ์์ ์๋ ํ์ผ๋ค ์ถ๊ฐ
echo build/*.log > .gitignore  // ํน์  ๋๋ ํ ๋ฆฌ(build) ์์ ์๋ log ์ถ๊ฐ
```
```
No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   b.txt
        new file:   style.css

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore  // logํ์ผ์ .gitignore์ ๋ค์ด๊ฐ
```
## ์ฐธ๊ณ 
- [๋๋ฆผ์ฝ๋ฉ ์ ํ๋ธ](https://www.youtube.com/watch?v=Z9dvM7qgN9s)
- https://velog.io/@grinding_hannah/Git-Git-%EC%82%AC%EC%9A%A9%EB%B2%95-%EB%B0%8F-%ED%84%B0%EB%AF%B8%EB%84%90-%EB%AA%85%EB%A0%B9%EC%96%B4-%EC%A0%95%EB%A6%AC
