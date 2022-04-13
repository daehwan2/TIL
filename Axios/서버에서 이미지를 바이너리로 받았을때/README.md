서버에서 이미지(png파일)를 바이너리 형태로 받아서 img태그에 넣으려고 하니 잘안되었다.

구글링중 해결방법을 발견하여 정리한다.

### 상황

![image](https://user-images.githubusercontent.com/53414542/163135768-728fafc8-694d-4749-a615-f2ea196a5423.png)

다음과 같이 axios.get으로 data를 받았는데 다음과 같은 바이너리 데이터였다.

백쪽에 물어보니 stream 형태로 그냥 쏴주었다고 한다. img태그에 그냥 넣어도 보고 했는데 안되는 문제였다.


### 해결

1. javascript에서 제공해주는 객체인 [Blob](https://developer.mozilla.org/ko/docs/Web/API/Blob)객체를 생성해서 그 안에 바이너리 데이터를 넣어준다.
2. 그리고 window.URL.createObjectURL() 함수로 Object url을 만든다.

```javascript
axios.get("url")
.then((res)=>{
  const blob = new Blob([res.data], { type: "image/png" });
  const url = window.URL.createObjectURL(blob);
  
}).catch(err=>console.log(err);
```
--- 
이렇게까지 했었는데 계속 안되어서 엄청 헤맸었다.

왜 안되나 했더니 **axios에 responseType을 지정해줬어야 했다**

```javascript
axios.get("url",{
responseType: "blob",
})
.then((res)=>{
  const blob = new Blob([res.data], { type: "image/png" });
  const url = window.URL.createObjectURL(blob);
  
}).catch(err=>console.log(err);
```
