# HTML 문법(1)

#### (링크)

```html
<h1>오늘의 명언</h1>
우리 모두는 <strong>자신의 힘</strong>으로 발견한 내용을 가장 쉽게 익힌다.
<a href="https://ko.wikipedia.org/wiki/%EB%8F%84%EB%84%90%EB%93%9C_%EC%BB%A4%EB%88%84%EC%8A%A4">(도널드 카누스)</a>            # <a></a> 태그명만으로는 태그가 불충분함
```

![image-20200920212037617](C:\Users\mgk04.DESKTOP-8Q51H2D\AppData\Roaming\Typora\typora-user-images\image-20200920212037617.png)





##### 링크를 클릭하면 새로운 탭이 열리면서 페이지가 열리게 하고싶다면?

```html
<h1>오늘의 명언</h1>
우리 모두는 <strong>자신의 힘</strong>으로 발견한 내용을 가장 쉽게 익힌다.
<a href="https://ko.wikipedia.org/wiki/%EB%8F%84%EB%84%90%EB%93%9C_%EC%BB%A4%EB%88%84%EC%8A%A4" target="_blank">(도널드 카누스)</a>

# target="_blank" 추가하기
```



##### 도널드커누스에 마우스를 올려놨을때 속성이 나타나게 하려면?!

```html
<h1>오늘의 명언</h1>
우리 모두는 <strong>자신의 힘</strong>으로 발견한 내용을 가장 쉽게 익힌다.
<a href="https://ko.wikipedia.org/wiki/%EB%8F%84%EB%84%90%EB%93%9C_%EC%BB%A4%EB%88%84%EC%8A%A4" target="_blank" title="전설적인 프로그래머">(도널드 카누스)</a>

# title="전설적인 프로그래머" 추가하기
# href 웹이 기존의 기술과 그분되는 중요한 특성
```



##### 태그목록

```html
<li>기술소개</li>
<li>기본문법</li>
<li>하이퍼텍스트와 속성</li>
<li>리스트와 태그의 중첩</li>
```

![image-20200920214640655](C:\Users\mgk04.DESKTOP-8Q51H2D\AppData\Roaming\Typora\typora-user-images\image-20200920214640655.png)

<li>태그는 <li>단독으로 사용되지않는다.



```html
<li>기술소개</li>
<li>기본문법</li>
<li>하이퍼텍스트와 속성</li>           #수업목록
<li>리스트와 태그의 중첩</li>

<li>최진혁</li>
<li>최유빈</li>					  #수업참여
<li>한이람</li>
<li>한이은</li>
```

![image-20200920214959152](C:\Users\mgk04.DESKTOP-8Q51H2D\AppData\Roaming\Typora\typora-user-images\image-20200920214959152.png)





##### 수업목록과 수업참여자가 시각적으로 구분되게 하고싶다면?

```html
<ul>
 <li>기술소개</li>
 <li>기본문법</li>            #ul을 사용하면 그룹핑한 효과가 나타난다
 <li>하이퍼텍스트와 속성</li>   #<ul> 태그가 묶여있는것 끼리 묶어짐
 <li>리스트와 태그의 중첩</li>  # 순서가 있는 항목
</ul>
<ul>
 <li>최진혁</li>
 <li>최유빈</li>              # 순서가 없는 항목
 <li>한이람</li>
 <li>한이은</li>
</ul>
```

![image-20200920215305411](C:\Users\mgk04.DESKTOP-8Q51H2D\AppData\Roaming\Typora\typora-user-images\image-20200920215305411.png)*태그안에 또다른 태그가 존재할수 있다*



```html
<ol>                        # ordered list (순서가 있는 리스트)
<li>기술소개</li>
<li>기본문법</li>
<li>하이퍼텍스트와 속성</li>   #list
<li>리스트와 태그의 중첩</li>
</ol>
<ul>                       # unordered list (순서가 없는 리스트)
<li>최진혁</li>
<li>최유빈</li>
<li>한이람</li>
<li>한이은</li>
</ul>
```

![image-20200920215746310](C:\Users\mgk04.DESKTOP-8Q51H2D\AppData\Roaming\Typora\typora-user-images\image-20200920215746310.png)



## 문서구조

```html
<html>
<head>
	<title>HTML-수업소개</title>  # 추가 된거 확인 #문서자체를 꾸며줌
	<meta charset="UTF-8">       # 글자 깨질때   #문서의 문자는 이런식으로 저장되어있다! 
</head>
<body>
<h1>HTML</h1>                # 웹브라우저의 본문에 해당        
<ol> 
`<li>기술소개</li>
`<li>기본문법</li>
`<li>하이퍼텍스트와 속성</li>
`<li>리스트와 태그의 중첩</li>
</ol>

<h2>선행학습</h2> 
<h2>수업의 목적</h2>      
</body>  
</html>
```

![image-20200920220501017](C:\Users\mgk04.DESKTOP-8Q51H2D\AppData\Roaming\Typora\typora-user-images\image-20200920220501017.png)