# Axios- Basic๐ฃ

### 1.์ค์น
```
npm install axios
yarn add axios
```

### 2. ์ฌ์ฉ
- import ํด์ฃผ๊ธฐ
```javascript
import axios from "axios";
```
- GET ์์ฒญ
```javascript
export const getPostsDB = () => {
  return async function(dispatch, getState) {
    try {
      dispatch(getLoading(true));
      const { data } = await axios.get("");  // ("")์์ API URL ๋ฃ๊ธฐ
      dispatch(getPostsSuccess(data));
    }
    catch (error) {
      dispatch(getError(true));
      alert("๋คํธ์ํฌ ์ค๋ฅ!")
    }
    finally {
      dispatch(getLoading(false));
    }
  }
}
```
- POST ์์ฒญ
```javascript
export const addPostDB = ({title, imgURL, text}) => {
  return async function(dispatch, getState) {
    try {
      dispatch(getLoading(true));

      axios.post("", {
        board_title : title,
        board_imgURL : imgURL,
        board_text : text,           // ""์์ API URL ๋ฃ๊ธฐ, ๋ ๋ฒ์งธ ํ๋ผ๋ฏธํฐ๋ก ์ถ๊ฐํ  data
      })
      dispatch(addPostSuccess());
    }
    catch(error) {
      dispatch(getError(true));
      alert("๋คํธ์ํฌ ์ค๋ฅ๋ก ๊ธ์ ์์ฑํ์ง ๋ชปํ์ด์ :(")
    }
    finally {
      dispatch(getLoading(true));
    }
  }
}
```
- DELETE ์์ฒญ
```javascript
export const deletePostDB = (id) => {
  return async function (dispatch, getState){
    try {
      dispatch(getLoading(true));
      await axios.delete(`http://localhost:4000/posts/${id}`);  // id๋ฅผ ๋ฐ์์ API URL์ ํด๋น id๋ถ๋ถ ์ญ์ 
      alert("๊ฒ์๊ธ์ด ์ญ์ ๋์์ต๋๋ค.");
    }
    catch(error) {
      dispatch(getError(true));
      alert("๋คํธ์ํฌ ์ค๋ฅ๋ก ๊ธ์ ์ญ์ ํ์ง ๋ชปํ์ด์ :(");
    }
    finally {
      dispatch(getLoading(false));
    }
  }
}
```
- PUT ์์ฒญ
๊ธฐ๋ฅ๊ตฌํ ํ ์ถ๊ฐ

### ์ฐธ๊ณ 
- [์์๊ธฐ ๋งค๋์ ๋ repo](https://github.com/with-key/hh99_axios_basic)
