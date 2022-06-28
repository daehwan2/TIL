https://velog.io/@leo-xee/React-Router%EC%9D%98-match-location-history-%EA%B0%9D%EC%B2%B4

글이 너무 잘정리되어 있어서 따라적으며 공부하였습니다.

# Router의 props
브라우저와 리액트 앱의 Router로 연결하면 Router가 history api에 접근할 수 있게 되고 

각 Route와 연결된 컴포넌트의 props로 match,location, history 객체를 기본적으로 전달하게 된다.

이 3가지 객체의 속성에 대해서 정리한다.

### App.js

```javascript
import React from "react";
import { Route } from "react-router-dom";
import Home from "./Home";
import About from "./About"

function App() {
  return (
    <div>
      <Route path="/" exact={true} component={Home} />
      <Route path="/about" component={About} />
    </div>
  );
}

export default App;
```

### Home.js

```javascript
import React from 'react';

const Home = (props) => {
  console.log(props);		// props 출력
  return (
    <div>
      <h1>홈</h1>      
      <p>이곳은 홈입니다.</p>
    </div>
  );
}

export default Home;
```

![image](https://user-images.githubusercontent.com/53414542/176185608-23b6b01e-a51b-46d4-85cc-a41607c2bb25.png)

<br/>
<br/>
<br/>
<br/>

## match
match 객체에는 Route path와 URL의 매칭에 대한 정보를 가지고 있다.

![image](https://user-images.githubusercontent.com/53414542/176185838-400d2972-07c7-4536-8b3e-41e3fe99fea3.png)

- isExact: true 이면 경로가 완전히 정확할 경우에만 수행한다.
- params: 경로에 전달된 파라미터 값을 가진 객체
- path: Route에 정의된 경로
- url: 클라이언트로부터 실제 요청 받은 경로

<br/>
<br/>

## location
location 객체는 현재 페이지에 대한 정보를 가지고 있다.

![image](https://user-images.githubusercontent.com/53414542/176186219-b936257b-0c3e-4ffa-9ace-bf0347630f49.png)

- hash: 현재 페이지의 hash 값
- pathname: 현재 페이지의 경로
- search: 현재 페이지의 hash값 ( 이를 사용해서 querystring을 가져올 수 있다.)

<br/>
<br/>

## history
history 객체는 브라우저의 history api에 접근한다.

![image](https://user-images.githubusercontent.com/53414542/176186443-eca0d89c-a4f7-4187-b364-a696d4a00ab7.png)

- action: 최근에 수행된 action(push, pop, replace)
- block(propt): history 스택의 push와 pop 동작을 제어
- go(n): history스택의 포인터를 n으로 이동
- goBack(): 이전페이지로 이동
- goForward(): 앞 페이지로 이동
- length: 전체 history스택의 길이
- location: 현재 페이지의 정보
- push(path, state): 새 경로를 history스택에 push 해서 페이지 이동
- replace(path,state): 최근 경로를 history 스택에서 replace해서 페이지 이동
