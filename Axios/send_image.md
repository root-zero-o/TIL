# formData 활용해서 이미지 post하기

### 1. 이미지만 보낼 때
#### 1) formData 객체 만들기
```javascript
const onChangeImg = (event) => {
  event.preventDefault();
  
  if(event.target.files){
    const uploadFile = event.target.files[0]
    const formData = new FormData()  // js 내장객체인 formData를 이용해 이미지파일을 formData 형식으로 만듦
    formData.append("files", uploadFile)  // append를 사용해 key와 value 넣기
  }
}
```
#### 2) 서버로 전송하기
```javascript
const onChangeImg = async (event) => {
  event.preventDefault();
  
  if(event.target.files){
    const uploadFile = event.target.files[0]
    const formData = new FormData()  // js 내장객체인 formData를 이용해 이미지파일을 formData 형식으로 만듦
    formData.append("files", uploadFile)  // append를 사용해 key와 value 넣기
    
    await axios ({
      method : "post",
      url: "/api/files/images",
      data : formData,
      headers : {
        "Content-Type" : "multipart/form-data"
      }  
    })
  }
}
```

----

### 파일(이미지)과 다른 data 같이 formData에 넣어서 post하기
- file은 multipart/form-data, data는 application/json 형식으로 보내기 위해 Blob 사용
```javascript
import React, { useState } from "react"
import { Button } from "antd"
import Axios from "axios"
import UploadImage from "./Sections/UploadImage"

const CreateList = () => {
  const [files, setFiles] = useState([])

  const user = useSelector(state => state.user)
  const history = useHistory()

  const onCreate = () => {
    let formData = new FormData()

    formData.append("file", files[0])

    let variables = [{
      title: "title",
      content: "content"
    }]

    formData.append("data", new Blob([JSON.stringify(variables)], {type: "application/json"}))
    
    Axios.post("/create/list", formData)
  }
  
  const onDrop = (files) => {
    setFiles(files)
  }

  return (
    <div>
      <UploadImage onDrop={onDrop} />
      <Button size="large" onClick={onCreate}>생성하기</Button>
    </div>
  )
}
export default CreateList
```


### 참고
- https://stackoverflow.com/questions/47630163/axios-post-request-to-send-form-data
- https://developer0809.tistory.com/135
