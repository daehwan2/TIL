처음에 기본 세팅을 할때마다 구글링을 찾아서 보고 있어서 기본 세팅에 대해 정리한다.

### 리액트에서 tailwindCSS 사용법

1. 라이브러리 설치
`npm i -d autoprefixer postcss tailwindcss`

2. postcss.config.js 작성 (package.json 과 같은 위치)
```javascript
module.exports = {
  plugins: [
    require("autoprefixer")({
      browsers: ["> 1%", "last 2 versions"],
    }),
  ],
};
```
3. tailwind.config.js 작성 (package.json 과 같은 위치)
```javascript
module.exports = {
  content: ["./src/**/*.{js,jsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
``` 
4. index.css 작성 (src폴더 하위에 위치)
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```
**`index.js`에서 index.css를 import 해줘야함**
`import "./index.css";`


---

이후에 클래스이름을 지정해주면서 바로 사용가능.
https://tailwindcss.com/ 사용법은 공식홈페이지에 잘나와있음.
