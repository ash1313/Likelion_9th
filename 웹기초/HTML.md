HTML

### HTML(Hyper Text Markup Language)

##### 클라이언트 <->서버 주고받는 파일

+ 이해가 쉬움
+ 정형화된 문법
+ 쓰이는 문법만 맨날 쓰임

Hyper Text = Link

Markup Language: 컴퓨터가 알아들을 수 있는 언어



#### HTML코드

1. 글
2. 태그
3. 속성



#### 과제 

+ Introduction to html 

+ 직접 쳐보는게 중요

+ HTML은 중요한 기초



#### 대원칙

+ HTML로 꾸미려 들지 말자(꾸미는 언어가 아님)
+ 꾸미는 언어는 CSS!



#### HTML 코드

1. "이거 HTML(로 작성된)문서야~"를 알려주는 태그

2. 직접 화면에 등장하진 않지만 이 문서를 설명하는 태그

   ex)이 문서를 한 마디로 설명하는 문서의 'Title', 인코딩 방식(utf-8)등등.

3. 직접적으로 화면에 등장하는, 문서에서 보이는 태그

   ex)h1, p, li, ...



#### 실습

VScode

! tap= 초기 설정

`````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
`````



+ form 태그

  ##### 사용자(form) -> HTML(form action="전송받을 대상")->전송받을 대상

+ ol(ul)>li*4

  ````html
  <ol(ul)>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
  </ol(ul)>
  ````

+ input 태그

  type : text, password, submit 

  `````html
  <input type="text" name="myid">
  `````

+ select 태그

  `````html
  <select>
      <option value="goodday">좋은날</option>
  </select>
  `````

+ img 태그

  `````html
  <img src="snowman.jpg" height=300>
  `````

+ br 태그

  `````html
  <br>
  `````

+ a 태그

  `````html
  <a href="1.html">유년기</a>
  `````

  

