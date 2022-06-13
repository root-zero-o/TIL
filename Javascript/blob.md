# Blob(블랍)

### 1. 개념
- Blob(Binary Large Object)은 이미지, 사운드, 비디오와 같은 멀티미디어 데이터를 다룰 때 사용할 수 있음
- 데이터의 크기(Byte) 및 MIME 타입을 알아내거나, 데이터를 송수신을 위한 작은 Blob 객체로 나누는 등의 작업에 사용함

----

### 2. 생성
```javascript
const newBlob = new Blob(array, options);
```
- ```array```
    - Blob 생성자의 첫 번째 인수
    - ArrayBuffet, ArrayBufferView, Blob(file), DOMString 객체 또는 이러한 객체가 혼합된 Array 사용 가능
- ```options```
    - ```type```과 ```endings```를 설정할 수 있음
    - ```type``` : 데이터의 MIME 타입을 결정, 기본값은 ```""```
    - ```endings```: ```\n```을 포함하는 문자열 처리를 ```"transparent```와 ```native```로 지정할 수 있음(기본값은 ```transparent```

----

### 3. Blob 객체
![콘솔](https://user-images.githubusercontent.com/97326130/173356643-a4eeed88-7911-43ff-ada7-ab9a9d53cedb.png)

- 생성자를 통해 만들어진 Blob 객체는 ```size```,```type```의 속성을 가짐
- ```size``` : Blob 객체의 Byte 단위 크기
- ```type``` : 객체의 MIME 타입, 알 수 없는 경우 빈 문자열이 할당됨


#### Methods - ```slice```
- 지정된 Byte 범위의 데이터를 포함하는 새로운 Blob 객체를 만듦
- 10MB 이상 사이즈가 큰 Blob 객체를 작게 조각내어 사용할 때 유용함

```javascript
const blob = new Blob();
blob.slice(start, end, type);
```
- ```start``` : 시작 범위(Byte, Number)
- ```end``` : 종료 범위(Byte, Number)
- ```type``` : 새로운 Blob 객체의 MIME 타입(String) 지정
```javascript
const chunk = blob.slice(0, 1024, "image/jpeg");  // Blob 객체에서 첫 1KB의 JPG Blob객체(chunk)를 생성
```
👉 조각낸 Blob 객체들은 필요에 의해 간단하게 다시 합칠 수 있음

----

### 4. Blob URL
- Blob 객체를 가리키는 URL을 생성하기 위해 ```createObjectURL```과 ```revokeObjectURL```을 사용할 수 있음
- ```URL.createObjectURL()``` 
    - Blob 객체를 나타내는 URL을 포함한 DOMString 생성
    - Blob URL은 생성된 window의 document에서만 유효하며, URL의 수명이 한정되어 있음
- ```revokeObjectURL()``` 
    - ```URL.createObjectURL()```을 통해 생성한 기존 URL을 해제(폐기)
    - 해제하지 않으면 기존 URL을 유효하다고 판단하여 메모리 누수가 일어날 수 있으니 DOM과 바인딩 후에 해제할 것!
```javascript
// Create Blob URL
const blobUrl = window.URL.createObjectURL(blob);

// Revoke Blob URL after DOM updates
window.URL.revokeObjectURL(blobUrl);
```

----
## 참고
- https://heropy.blog/2019/02/28/blob/

