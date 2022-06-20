# forwardRef

## 1. 💁‍♀️ 언제 사용하지 ?

- ```ref```를 ```컴포넌트```에 사용하고 싶을 때 사용 !
    - 함수 컴포넌트는 ref가 존재하지 않기 때문에 ref를 통해 함수 컴포넌트를 제어할 수 없음

## 2. 사용방법

### 상황 
- ```home.js``` 파일에서 스크롤 애니메이션을 사용하고 싶다.
- 그런데 스크롤 애니메이션을 사용하고 싶은 요소의 위치는 ```mainImage.jsx```라는 컴포넌트 안에 위치해 있다.

### 사용방법
- 일단 하위 컴포넌트인 ```mainImage.jsx``` 를 ```forwardRef```로 묶어주기
```javascript
const MainImage = forwardRef(({Img, MobileImg, title, text, btn1, btn2}, section2Ref) => {  
                                                              // 두번째 파라미터가 ref

    const { ref, inView } = useInView({
        threshold: 0.5  
      });
    
  return (
    <StContainer ref={section2Ref}>  // ref를 사용하고 싶은 태그에 요렇게 붙여주기
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
- 상위 페이지인 ```home.js```에서 ```useRef()``` 사용해 ref 끌어와 사용하기 !
```javascript
 const section2Ref = useRef();
 
 const onClickSection2 = () => {
    const section2Top = section2Ref?.current?.getBoundingClientRect().top
    window.scrollBy({top: section2Top, behavior: 'smooth'})
  }
```
