# Git Settings๐ 

## 1. Initial Settings

**์ค์  ํ์ธ**
```
git config --list 
```
**์ค์  ํ์ธ(file)**
```
git config --global -e
```
**VSCode๋ก ์ด๊ธฐ**
```
git config --global core.editor "code" // VSCode๊ฐ ์ด๋ฆฌ๋ฉด์ ๋์์ ๋ค๋ฅธ ๋ช๋ น์ด ์คํํ  ์ ์๋๋ก ํฐ๋ฏธ๋ ํ์ฑํ ๋จ
git config --global core.editor "code --wait" // ์ด๋ฆฐ VSCode๊ฐ ์ข๋ฃ๋๊ธฐ ์ด์ ์ ๋ค๋ฅธ ๋ช๋ น์ด ์ํX
git config --global -e // VSCode ์ด๊ธฐ
```

## 2. ์ฌ์ฉ์ ์ ๋ณด ์ค์ 
```
git config --global user.name "์ด๋ฆ"  // ์ฌ์ฉ์ ์ด๋ฆ ์ค์ 
git config --global user.email "์ด๋ฉ์ผ์ฃผ์"  // ์ฌ์ฉ์ ์ด๋ฉ์ผ ์ค์ 
git config user.name // ์ด๋ฆ ํ์ธ
git config user.email // ์ด๋ฉ์ผ ํ์ธ
```
```
git config --global core.autocrlf true // Mac์ true ๋์  input 
```
- ์ด์์ฒด์ ๋ง๋ค ์ค๋ฐ๊ฟ ๋ฐฉ์์ด ๋ฌ๋ผ ๋ฌธ์ ๊ฐ ์๊ธธ ์ ์์
- ์ด๋ฅผ ์ด์์ฒด์ ๋ง๋ค ๊น์์ ์์ ํด์ ์ ์ฅ ๋ฐ ๋ถ๋ฌ์ค๊ธฐ ํด์ค!

## ์ฐธ๊ณ 
- [๋๋ฆผ์ฝ๋ฉ ์ ํ๋ธ](https://www.youtube.com/watch?v=Z9dvM7qgN9s)
