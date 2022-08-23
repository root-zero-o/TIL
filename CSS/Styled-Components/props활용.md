# props 활용 
같은 h2 태그를 가진 element를 사용해야 한다고 가정할 때, 폰트사이즈만 다르게 하고 싶다면?
```javascript
const SubTitleFont = styled.h2`
    font-size: ${(props) => props.fontSize}; // 2. 넘겨받은 prop 안의 fontSize가 입력됨
    font-weight: 600;
`

fuction App () {
	return (
    	<section>
        	<SubTitleFont fontSize="22px">부제목1</SubTitleFont> // 1. SubtitleFont에 props로 fontSize를 줌
            <SubTitleFont fontSize="24px">부제목2</SubTitleFont>
        </section>
    )
}
```
