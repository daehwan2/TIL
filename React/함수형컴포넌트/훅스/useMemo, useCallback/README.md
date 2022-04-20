미리 알아야할 것.
1. 함수형 컴포넌트는 jsx를 반환하는 함수이다.
2. 컴포넌트 렌더링한다는 것은 함수(컴포넌트가)가 실행된다는 것.
3. **함수가 실행될때마다 내부에 선언되어 있던 표현식(변수, 함수) 등이 매번 다시 선언된다.**
4. 컴포넌트는 자신의 state가 변경되거나 부모에게서 받은 props가 변경되었을때마다 리렌더링 된다.
  **( 심지어 하위컴포넌트에 최적화 설정을 해주지 않으면 부모에게서 받는 props가 변경되지 않았더라도 리렌더링 되는게 기본이다.)**

# useMemo

**성능 최적화를 위하여 연산된 값을 재사용하는 기능을 가진 함수**
**memorization된 값을 반환한다.**
```jsx
//App.js

import React, { useState } from "react";
import ShowState from "./ShowState";

const App = () => {
  const [number, setNumber] = useState(0);
  const [text, setText] = useState("");

  const increaseNumber = () => {
    setNumber((prevState) => prevState + 1);
  };

  const decreaseNumber = () => {
    setNumber((prevState) => prevState - 1);
  };

  const onChangeTextHandler=(e)=>{
    setText(e.target.value);
  }

  return (
    <div className="App">
      <div>
        <button onClick={increaseNumber}>+</button>
        <button onClick={decreaseNumber}>-</button>
        <input
          type="text"
          placeholder="Last Name"
          onChange={onChangeTextHandler}
        />
      </div>
      <ShowState number={number} text={text} />
    </div>
  );
};
```
```jsx
//ShowState.js

import React from "react";
import "./styles.css";

const getNumber = (number) => {
  console.log("숫자가 변동되었습니다.");
  return number;
};

const getText = (text) => {
  console.log("글자가 변동되었습니다.");
  return text;
};

const ShowState = ({ number, text }) => {
  const showNumber = getNumber(number);
  const showText = getText(text);

  return (
    <div className="info-wrapper">
      {showNumber} <br />
      {showText}
    </div>
  );
};

export default ShowState;
```


이때 App 컴포넌트에서 ShowState컴포넌트로 인자를 두개를 주고있는데 이중 하나만 바뀌어도 ShowState의 모든게 리렌더링 된다.
그렇게 때문에 위의 코드에서 state를 아무거나 하나 바꾸게되면
console 창에 
```
숫자가 변동되었습니다.
글자가 변동되었습니다.
```
두개가 뜰것이다.

**하나만 바뀌는데 ShowState전체가 리렌더링 되기때문에 발생하는 현상이다.**

이때 바뀌는 인자에 관한것만 렌더링해주는 것이 useMemo 이다. 앞의 예제는 다음과 같이 바꿀 수 있다.

```jsx
//ShowState.js

import React,{useMemo} from "react";
import "./styles.css";

const getNumber = (number) => {
  console.log("숫자가 변동되었습니다.");
  return number;
};

const getText = (text) => {
  console.log("글자가 변동되었습니다.");
  return text;
};

const ShowState = ({ number, text }) => {
  const showNumber = useMemo(()=>getNumber(number),[number]);
  const showText = useMemo(()=>getText(text),[text]);

  return (
    <div className="info-wrapper">
      {showNumber} <br />
      {showText}
    </div>
  );
};

export default ShowState;
```

# useCallback
**memorization된 함수를 반환한다.**
**특정함수를 새로만들지 않고 재사용하고 싶을때 사용한다.**
```jsx
//App.js

import React, { useState } from "react"
import List from "./List"

function App() {
  const [number, setNumber] = useState(1)
  const [dark, setDark] = useState(false)

  const getItems = () => {
    return [number, number + 1, number + 2]
  }

  const theme = {
    backgroundColor: dark ? "#333" : "#fff",
    color: dark ? "#fff" : "#333",
  }

  return (
    <div style={theme}>
      <input
        type="number"
        value={number}
        onChange={e => setNumber(parseInt(e.target.value))}
      />
      <button onClick={() => setDark(prevDark => !prevDark)}>테마 변경</button>
      <List getItems={getItems} />
    </div>
  )
}

export default App
```

```jsx
//List.js

import React, { useEffect, useState } from "react"

export default function List({ getItems }) {
  const [items, setItems] = useState([])
  useEffect(() => {
    setItems(getItems())
    console.log("숫자가 변동되었습니다.")
  }, [getItems])
  return items.map((item, index) => <div key={index}>{item}</div>)
}
```

이 때 List 컴포넌트가 props로 App컴포넌트의 getItems를 받고 있으므로 테마가 변경되는 버튼을 클릭할때마다
console에
```
숫자가 변동되었습니다.
```
가 찍히게 된다. 

**부모 컴포넌트가 리렌더링되면서 자식컴포넌트의 props가 변경되었다고 인식되는 것이다.**

이 때 App.jsx에 useCallback 을 사용하면 이를 고칠 수 있다.

```jsx
//App.js

import React, { useState, useCallback } from "react"
import List from "./List"

function App() {
  const [number, setNumber] = useState(1)
  const [dark, setDark] = useState(false)

  const getItems = useCallback(() => {
    return [number, number + 1, number + 2]
  }, [number])

  const theme = {
    backgroundColor: dark ? "#333" : "#fff",
    color: dark ? "#fff" : "#333",
  }

  return (
    <div style={theme}>
      <input
        type="number"
        value={number}
        onChange={e => setNumber(parseInt(e.target.value))}
      />
      <button onClick={() => setDark(prevDark => !prevDark)}>테마 변경</button>
      <List getItems={getItems} />
    </div>
  )
}

export default App
```


참조 사이트
https://velog.io/@kysung95/%EC%A7%A4%EB%A7%89%EA%B8%80-useCallback%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EC%9E%90
https://velog.io/@kysung95/%EC%A7%A4%EB%A7%89%EA%B8%80-useMemo
