# 1900 static site
서버에 html 파일이 있고 client가 요청하면 html파일을 가져와서 보여줌.

페이지내에서 다른 링크를 클릭하면 새로운 html 파일을 가져와서 뿌려주기 때문에 새로고침이 됨.

# 1996 iframe 태그 도입
iframe 태그 : 페이지 내에서 부분적으로 문서를 받아와서 업데이트 가능해짐.

# 1998 XMLHttpRequest API 개발
html 문서 전체가 아니라 json등등의 포맷으로 서버에서 필요한 데이터만 받아올 수 있음.

1. 데이터를 받음
2. javascript를 이용해서 동적으로 html 요소를 생성.
3. 페이지 업데이트

# 2005 AJAX
사용자가 한페이지 내에 머물면서 필요한 데이터만 서버에서 받아와서 부분적으로만 업데이트 함.
SPA ( Single Page Application )

# CSR ( Client Side Rendering )
자바스크립트가 표준화가 잘되고, 리액트, 앵귤러, 뷰등이 나오면서 가능해짐.

1. 서버에서 index.html 을 클라이언트로 보내줌.
예제) index.html
```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="utf-8" />
  </head>
  <body>
    <div id="root"></div>
    <script src="app.js"></script>
  </body>
</html>
```
빈화면만 띄워짐.

2.  app.js 서버에서 가져옴. 이때 app.js 에 프레임워크의 모든것등등이 다 담겨있음.
3.  필요한 데이터를 json등의 형태로 서버에서 가져옴.
4. 렌더링.

### ⚠️  문제점
- 사용자가 첫 화면을 보기까지 오래걸림( app.js가 큰 파일이기 때문에 )
- SEO (Search Engine Optimization) 안좋음.

# SSR(Server Side Rendering)
1. 서버에서 필요한 데이터를 모두 가져와서 html파일을 만듬.
2. 서버에서 만들어진 html파일과 html파일을 동적으로 조금 제어할 수 있는 소스코드와 함꼐 클라이언트로 보냄.

- CSR 보다 첫번째 페이지로딩이 빠름.
- 모든 컨텐츠가 html 파일에 들어있기 때문에 조금 더 효율적인 SEO를 할 수 있다.

### ⚠️ 문제점
- static sites에서 발생했던 문제인 blinking issue가 발생한다.  전체적인 웹사이트를 다시 서버에서 가져오는 것과 동일함.
- 서버에 과부화가 걸림. ( 사용자가 클릭을 할때마다 서버에 요청해서 html을 만들어서 클라이언트로 줘야하기 때문에 )
- 사용자가 빠르게 웹사이트를 확인할 수는 있지만 동적으로 데이터를 처리하는 js를 받지못해서 클릭했을때 반응이 없을 수도 있음. ( TTV, TTI )

# TTV ( Time To View ), ( Time To Interact ) 
![image](https://user-images.githubusercontent.com/53414542/164032738-b44ec149-6697-4b52-b233-38bc7de2a426.png)

TTV와 동시에 TTI가 가능함 => 사용자가 view를 봄과 동시에 상호작용이 가능함!

![image](https://user-images.githubusercontent.com/53414542/164033022-bdfb47a5-1d49-4016-a68b-fe5492e869fb.png)

TTV가먼저 되고 TTI는 나중. 텀이있음


# SSG ( Static Site Generation )
React + Gatsby
![image](https://user-images.githubusercontent.com/53414542/164033579-fd83b7b4-539c-4364-9406-098b1d26868b.png)

React + Next.js
![image](https://user-images.githubusercontent.com/53414542/164033843-a8c585fa-ae17-4a3e-81e7-6d7899aa9a43.png)


참고영상 https://www.youtube.com/watch?v=iZ9csAfU5Os&t=30s
