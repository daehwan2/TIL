## Selenium

https://www.selenium.dev/documentation/

웹 테스트 자동화 도구. 크롤링에서도 많이 쓰인다.

웹상의 업무 자동화도 가능

---

nodejs 에서 간단 사용법.

크롬에서 사용할 경우 `chromedriver`와 `selenium-webdriver`를 설치한다

`npm i selenium-webdriver`
`npm i chromedriver`

```javascript
require("chromedriver");
var { Builder, By, Key, until } = require("selenium-webdriver");
const chrome = require("selenium-webdriver/chrome");
const chromeOptions = new chrome.Options();
    chromeOptions.excludeSwitches("enable-logging");
    var driver = new Builder()
      .forBrowser("chrome")
      .setChromeOptions(chromeOptions)
      .build();

(async function helloSelenium() {
  try {
    await driver.get("https://www.naver.com"); //크롬드라이버가 창을띄워서 만들어줌.

// 원하는 태그를 id, class, name 등으로 찾아서 이벤트를 다룰 수 있음. 자세한 사용법은 공식문서에 자세히 나와있어서 생략.
}catch(err){
console.log(err)
}
})();
```


ex) code-etc-worldcup-frontend에서 필요해서 사용해보게 되었다.

https://github.com/code-etc/code-etc-worldcup-frontend/issues/23

