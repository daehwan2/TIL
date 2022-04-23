
### **width %를 기준으로 한다.**


어떠한 상황에서 쓰이냐면 width가 가변적이고 height는 그 width와 같이 하고 싶을때

즉 정사각형을 만들고 싶을때 다음과 같이 사용할 수 있다.

```css
.product-card{
  width:calc(50% - 10px); //가변적인 width
  height:0;
  padding-bottom:100%;  // width와 같은 height를 가지게됨.
}
```
