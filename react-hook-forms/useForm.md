# useForm으로 유효성 검사하기

- 먼저 사용할 것들 ```useForm()```에서 꺼내주기
```javascript
const { register, handleSubmit, formState: {errors, isValid}, control} = useForm({
    mode: "onChange",  // 모드를 정할 수 있음
    defaultValues : {
      "nation": "",
      "firstName" : "",
      "lastName" : "",
      "userName" : "",
      "password" : ""   // defaultValue를 정할 수 있음
    }
  });
```

- submit 된 데이터 받기
```javascript
const onSubmit = (data, e) => console.log(data, e);  // console.log 부분에서 데이터 전송
                                                    // 유효성 검사를 통과하지 못하면 data 대신 errors가 return됨
```

- errors ?
    - 유효성 검사를 통과하지 못하면 통과하지 못한 이유를 알려줌(Object 형태)
    - 통과하지 못한 이유는 ```type : "" ``` 형태로 알려주고, type은 내가 정한 rule의 key값
    - 예를 들어, 아래 예시에서 ```required : true``` 였다면, input을 채우지 않으면 ```{ type: required, ... }```가 리턴됨


- 유효성 검사 결과 보여주기 : errors.type에 따라 달라지도록(옵셔널 체이닝 필요)
```javascript
<StInput type="text" {...register("firstName", { required: true, maxLength: 20 })}/>
   { errors.firstName?.type === "required" ? 
      <StAlertBox>
         <FontAwesomeIcon icon={faTriangleExclamation} style={{color:"tomato"}}/>
          <StAlert color="tomato">First Name is required.</StAlert>
       </StAlertBox>
          : null }
    { errors.firstName?.type === "maxLength" ? 
        <StAlertBox>
           <FontAwesomeIcon icon={faTriangleExclamation} style={{color:"tomato"}}/>
           <StAlert color="tomato">First Name is too long.(Max Length : 20)</StAlert>
         </StAlertBox>
           : null }
     {errors.firstName?.type === undefined ? 
        <StAlertBox>
           <FontAwesomeIcon icon={faCircleCheck} style={{color:"green"}}/>
           <StAlert color="green">Nice First name!</StAlert>
         </StAlertBox>
            : null }
```

## 참고
- https://react-hook-form.com/get-started#Registerfields
