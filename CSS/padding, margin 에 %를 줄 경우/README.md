
### **width %를 기준으로 한다.**


어떠한 상황에서 쓰이냐면 width가 가변적이고 height는 그 width와 같이 하고 싶을때

즉 정사각형을 만들고 싶을때 다음과 같이 사용할 수 있다.

#### html
```html
<div>
  <img src="dd.jpg" />
</div>
```

#### css
```css
div{ 
  position: realtive; // absolute 기준위해
  width:calc(50% - 10px); //가변적인 width
  height:0;
  padding-bottom:100%;  // width와 같은 height를 가지게됨.
}

div img{
  position:absolute;
  top:0;
  left:0;
  transform: translate(-50%, -50%);
  
  width:100%;
  height:100%;        // 부모의 height가 사실상 0이기 때문에 제대로된 이미지를 띄우지 못한다. 
                      // 이때 postion absolute를 설정하면 height가 정상적으로 작동한다. 그래서 중앙정렬시켜준다.
}
```


관련 커밋 578e43fabfe02e1ccf6e2360b3de48d36abbca51
