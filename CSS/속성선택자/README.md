CSS 선택자중 태그안에 속성까지 선택이 가능한 선택자가 있었다

# 속성 선택자
| 선택자       | 기능        | 하이폰(-) | 언더바(_) | 공백 | 합성어 |
| ------------ | ----------- | --- | -----------| ---- | ----- | 
| [attribute] | [속성명]     | X |  X  |  X    |    X |
| [attribute = "value"] | [속성명 + 속성값]     | X |  X  |  X    |    X |
| [attribute ~= "value] | [속성명 + 특정문자 들어간 속성값]     | X |  X  |  O    |    X |
| [attribute *= "value] | [속성명 + 특정문자 들어간 속성값]     | O |  O  |  O    |    O |
| [attribute \|= "value] | [속성명 + 접두사로 시작하는 속성값]     | O |  X  |  X    |    X |
| [attribute ^= "value] | [속성명 + 접두사로 시작하는 속성값]     | O |  O  |  O    |    O |
| [attribute $= "value] | [속성명 + 접미사로 시작하는 속성값]     | O |  O  |  O    |    O |

```css
button[disabled]{
  color:white;
}
```
