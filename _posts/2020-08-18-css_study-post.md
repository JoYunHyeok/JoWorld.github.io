---
title: "CSS 공부하기(1)"
excerpt: "생활코딩"

categories:
  - WEB
tags:
  - HTML
  - CSS
  - 생활코딩

last_modified_at: 2020-08-18
---
##CSS 공부하기
생활코딩에 있는 WEB2강의를 보며 공부한 내용을 정리하였습니다.

css를 배우는 이유는 여러개의 태그를 묶어 한번에 효율적으로 변경이 가능하다.
___

**css정리**
- font : HTML에 태그를 추가하는 방법 color를 변경하게 해줍니다.

- head에 style태그를 추가하여 css작업을한다.
- selector(선택자)와 Declaration(효과)
```
a{ //Selector
  color: red //Declaration
}
color -> Property
red -> Value
```
<br>

- 웹페이지에 css효과를 삽입하는 두가지방법
  - style태그를 쓴다.
  - style속성을 쓴다.
<br>

- css속성을 스스로 알아내는 방법
  - text의 사이즈를 키우거나 가운데 정렬하고 싶다면 'css text size Property', css text center Property'이런 식으로 검색하기
<br>

- css선택자를 스스로 알아내는 방법
  - 태그 < class < id 선택자 순으로 강하다. 이유는 id는 한번만 등장 가능(중복 불가능) 다른 곳에서 id값이 나오면 안된다.
<br>
- 박스 모델(box model)
  - 화면전체를 쓰는태그 = block
  - 자기 자신만큼의 크기를 쓰는 태그 = inline elemnet
  - block과 inline은 display라는 property의 default value일 뿐이다.(언제든지 변경가능)
  - padding : 컨텐트와 테두리 사이의 간격
  - margin : 테두리와 테두리 사이의 간격
  - width : 지정한 px만큼 element의 크기가 변경
<br>
- 그리드의 기본 사용법
  - div, span : block이냐 inline이냐에 따라서 골라쓴다. (디자인을 위함)
<br>
