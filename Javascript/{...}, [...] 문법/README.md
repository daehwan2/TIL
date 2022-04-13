# {...}, [...] 문법

- react에서 setState를 이용할때 많이 사용하고 있는데 헷갈려서 정리한다.
- es6에 추가된 문법이다.

### 비구조화 할당(= 구조분해 할당)
배열이나 객체 속성을 해체하여 개별 변수에 값을 담을 수 있는 JavaScript 표현식을 말합니다.


ex)
```javascript
let [x,y] = [1,2];
let {a,b} = {a: 1, b:2};
```

### 복사
1. 배열
```javascript
var arr = [1,2,3];
var copy1 = arr;
var [...copy2] = arr;
var copy3 = [...arr];

arr[0] = 'String';
console.log(arr); // [ 'String', 2, 3 ]
console.log(copy1); // [ 'String', 2, 3 ]
console.log(copy2); // [ 1, 2, 3 ]
console.log(copy3); // [ 1, 2, 3 ]
```

2. 객체
```javascript
var prevState = {
  name: "yuddomack",
  birth: "1996-11-01",
  age: 22
};

var state = {
  ...prevState,
  age: 23
};

console.log(state); 
```
