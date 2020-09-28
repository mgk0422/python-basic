# HTML

<html>

```html
<div class="box">박스</div>
<a href="google.com">구글</a>

1.<div></div>는 태그라고 하고 항상 열림/닫힘 한 쌍이 있음
2. class="box"은 속성이라고 함. 이 class속성을 이용해서 나중에 CSS로 스타일링을 할 수 있음
3. 합쳐서 "엘레먼트"라고 부름
```

```html
<!doctype html>
<html lang="en">
 <head>
	<title>테크보이 워니</title>
	<link href="style.css" #파일위치 rel="stylesheet" type="text/css"/> #파일이 어떤타입인지
	<meta name="description" content="테크보이 워니의 문서">
	# 카카오등 소셜미디어에 공유 될때 보여짐
	<style>
		.item{
		color : red;
		}
		.top{
		background : red;
		height : 100px;
		}
		.mid{
		background : black;
		height : 100px;
		}
		.bot{
		background : yellow;
		height : 100px;
		}
	</style>
 </head>
 <body>
	<div class="item">안녕<div>
	<!----------텍스트 관련 태그들------->
	<h1>안녕하세요</h1>
	<h2>안녕하세요</h2>
	<h3>안녕하세요</h3>
	<h4>안녕하세요</h4>
	<h5>안녕하세요</h5>
	<h6>안녕하세요</h6>
	<b>굵은글씨</b>
	<i>기울은글씨</i>
	<p>안녕하세요 저는 테크보이 워니입니다.</p>
	<!----------미디어 관련 태그들------->
	<img scr=""/>
	<video src="" controls> 
	<!----------링크 태그------->
	<a bref="google.com">구글</a>
	<a bref="facebook.com" target="_blank">페이스북</a> 
	#새창을 하나 더 띄움
	<!----------테이블 태그------->
	<table border="1">
		<thead>
			<tr>
			    <th>이름</th>
			    <th>나이</th>
			</tr>
		</thead>
		<tbody>
		    <tr>
			    <th>워니</th>
			    <th>3살</th>
		   </tr>
		   	<tr>
			    <th>제니</th>
			    <th>1살</th>
		   </tr>
		</tbody>
	</table>
	<!----------테이블 태그------->
	<ol> #order list
		<li>워니</li>
		<li>제니</li>
	</ol>
	<ul> #under list
		<li>워니</li>
		<li>제니</li>
	</ul>
	<!----------구역을 나누는 태그------->
	<div class="top">상단</div>
	<div class="mid">중단</div>
	<div class="bot">하단</div> #한줄 전체 공간을 차지
	<span class="like">좋아요</div>
    <span class="sub">구독</div>
    <span class="comment">댓글</div>
	<!----------인풋 태그------->
	텍스트 <input type="text"/>
	체크박스<input type="checknbox"/>
	라디오<input type="radio"/>
	색깔<input type="color"/>
	여러문장 <textarea></textarea>
	드랍다운 <selelct name='name'>
		<option value="워니">워니</option>
		<option value="제니">제니</option>
	</select>
	<form>
		<input type="email" placeholder="이메일" />
		<input type="password" placeholder="비밀번호" />
		<button type="submit">로그인</button>
	</form>
 </body>
</html>
```

<img src="C:\Users\mgk04.DESKTOP-8Q51H2D\Desktop\HTML.assets\image-20200917235825214.png" alt="image-20200917235825214" style="zoom:50%;" />

<img src="C:\Users\mgk04.DESKTOP-8Q51H2D\Desktop\HTML.assets\image-20200917235911336.png" alt="image-20200917235911336" style="zoom:50%;" />

