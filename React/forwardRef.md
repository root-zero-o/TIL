# forwardRef

## 1. ๐โโ๏ธ ์ธ์  ์ฌ์ฉํ์ง ?

- ```ref```๋ฅผ ```์ปดํฌ๋ํธ```์ ์ฌ์ฉํ๊ณ  ์ถ์ ๋ ์ฌ์ฉ !
    - ํจ์ ์ปดํฌ๋ํธ๋ ref๊ฐ ์กด์ฌํ์ง ์๊ธฐ ๋๋ฌธ์ ref๋ฅผ ํตํด ํจ์ ์ปดํฌ๋ํธ๋ฅผ ์ ์ดํ  ์ ์์

## 2. ์ฌ์ฉ๋ฐฉ๋ฒ

### ์ํฉ 
- ```home.js``` ํ์ผ์์ ์คํฌ๋กค ์ ๋๋ฉ์ด์์ ์ฌ์ฉํ๊ณ  ์ถ๋ค.
- ๊ทธ๋ฐ๋ฐ ์คํฌ๋กค ์ ๋๋ฉ์ด์์ ์ฌ์ฉํ๊ณ  ์ถ์ ์์์ ์์น๋ ```mainImage.jsx```๋ผ๋ ์ปดํฌ๋ํธ ์์ ์์นํด ์๋ค.

### ์ฌ์ฉ๋ฐฉ๋ฒ
- ์ผ๋จ ํ์ ์ปดํฌ๋ํธ์ธ ```mainImage.jsx``` ๋ฅผ ```forwardRef```๋ก ๋ฌถ์ด์ฃผ๊ธฐ
```javascript
const MainImage = forwardRef(({Img, MobileImg, title, text, btn1, btn2}, section2Ref) => {  
                                                              // ๋๋ฒ์งธ ํ๋ผ๋ฏธํฐ๊ฐ ref

    const { ref, inView } = useInView({
        threshold: 0.5  
      });
    
  return (
    <StContainer ref={section2Ref}>  // ref๋ฅผ ์ฌ์ฉํ๊ณ  ์ถ์ ํ๊ทธ์ ์๋ ๊ฒ ๋ถ์ฌ์ฃผ๊ธฐ
        <StMainImg Img={Img} MobileImg={MobileImg}>
            <StImgContent inView={inView}>
                <StTitleBox>
                    <StTitle>{title}</StTitle>
                    <StText>{text}</StText>
                </StTitleBox>
                <MainBtn btn1={btn1} btn2={btn2}/>
            </StImgContent>
            <StInViewBox ref={ref}/>
        </StMainImg>
    </StContainer>
    
  )
})
```
- ์์ ํ์ด์ง์ธ ```home.js```์์ ```useRef()``` ์ฌ์ฉํด ref ๋์ด์ ์ฌ์ฉํ๊ธฐ !
```javascript
 const section2Ref = useRef();
 
 const onClickSection2 = () => {
    const section2Top = section2Ref?.current?.getBoundingClientRect().top
    window.scrollBy({top: section2Top, behavior: 'smooth'})
  }
```
