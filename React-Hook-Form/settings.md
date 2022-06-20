# 🛠 Settings 🛠

- 설치
```
npm install react-hook-form
```

- import
```javascript
import { useForm } from "react-hook-form";
```

- Example
```javascript
export default function App() {
  const { register, handleSubmit, formState: { errors } } = useForm();  // 사용할 것들 꺼내기
  const onSubmit = data => console.log(data);  // data(객체형태) 가지고 작업 

  return (
    <form onSubmit={handleSubmit(onSubmit)}>  // handleSubmit이 onSubmit이 일어나기 전에 유효성 검사를 해줌
      <input defaultValue="test" {...register("example")} />  // register function을 사용해서 "example" key안에 input value 넣기
      <input {...register("exampleRequired", { required: true })} />  // {required} 등 유효성검사 기준을 만들 수 있음
      {errors.exampleRequired && <span>This field is required</span>}  // 유효성검사 실패하면 errors가 return됨
                                                                        // 여기서 errors는 객체!
      
      <input type="submit" />
    </form>
  );
}
```

## 참고
- https://react-hook-form.com/get-started
