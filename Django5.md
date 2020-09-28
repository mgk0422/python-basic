# Django 

수정

링크 클릭해서 들어가는건 GET방식이다.

자기 계정으로 들어갔을 때 상세 정보 확인



* 수정 버튼 생성

```python
<read.html>

<script>
				
$(document).ready(function(){
	$('#listBtn').click(function(){
		location.href='../bbs_list';
	})
	$('.btn-danger').click(function(){
		$('#removeFrm').attr('action','../bbs_remove/');
		$('#removeFrm').submit(); //$('#removeFrm')이것은 폼태그 / 폼태그에 submit를 추가해준다
	})
  	$('.btn-warning').click(function(){
      alert('modify btn click')
   	})
});

</script>
```

* 수정 할 수있는 페이지로 이동

```python
<urls.py>

urlpatterns = [
    path('index/', views.loginForm, name='loginForm'),
    path('registerForm/', views.registerForm, name='registerForm'),
    path('register/', views.register, name='register'),
    path('login/', views.login, name='login'),
    path('logout/', views.logout, name='logout'),
    path('bbs_list/', views.list, name='bbs_list'),
    path('bbs_registerForm/', views.bbsRegisterForm, name='bbs_registerForm'),
    path('bbs_register/', views.bbsRegister, name='bbs_register'),
    path('bbs_read/<int:id>', views.bbsRead, name='bbs_read'),
    path('bbs_remove/', views.bbsRemove, name='bbs_remove'),
    path('bbs_modifyForm/', views.bbsModifyForm, name = 'bbs_modifyForm'), # 추가
]
```

* 데이터 뿌리기

```python
<view.py>

def bbsModifyForm(request):
    id = request.POST['id']
    bbs = Bbs.objects.get(id=id)
    context = {'bbs': bbs,'name' : request.session['user_name'], 'id' : request.session['user_id']}
    return render(request,'modify.html', context)
```

* id writer은 고정, title content만 수정

```python
	<div class="box-body">

		<div class="form-group">
			<label for="exampleInputEmail1">ID</label> <input type="text"
				name='id' class="form-control" value="{{bbs.id}}"
				readonly="readonly">
		</div>

		<div class="form-group">
			<label for="exampleInputEmail1">Title</label> <input type="text"
				name='title' class="form-control" value="{{bbs.title}}">
		</div>
		<div class="form-group">
			<label for="exampleInputPassword1">Content</label>
			<textarea class="form-control" name="content" rows="3">{{bbs.content}}</textarea>
		</div>
		<div class="form-group">
			<label for="exampleInputEmail1">Writer</label> <input
				type="text" name="writer" class="form-control"
				value="{{bbs.writer}}"
				readonly="readonly">
```



* 게시글 수정하기

```python
<urls.py>

urlpatterns = [
    path('index/', views.loginForm, name='loginForm'),
    path('registerForm/', views.registerForm, name='registerForm'),
    path('register/', views.register, name='register'),
    path('login/', views.login, name='login'),
    path('logout/', views.logout, name='logout'),
    path('bbs_list/', views.list, name='bbs_list'),
    path('bbs_registerForm/', views.bbsRegisterForm, name='bbs_registerForm'),
    path('bbs_register/', views.bbsRegister, name='bbs_register'),
    path('bbs_read/<int:id>', views.bbsRead, name='bbs_read'),
    path('bbs_remove/', views.bbsRemove, name='bbs_remove'),
    path('bbs_modifyForm/', views.bbsModifyForm, name = 'bbs_modifyForm'),
    path('bbs_modify/', views.bbsModify, name='bbs_modify'),
]
```

```python
<views.py>

def bbsModify(request) :
    id = request.POST['id']         id title content 받아오기.
    title = request.POST['title']
    content = request.POST['content']

    bbs = Bbs.objects.get(id=id)   #Bbs 테이블에서 거기에 해당하는 id데이터를 불러온다

    bbs.title = title  #객체속성 / 접근 원래 테이블에 잇던 title 출력
    bbs.content = content
    bbs.save()

    context = {'bbs': bbs, 'name': request.session['user_name'], 'id': request.session['user_id']}

    return redirect('bbs_list')
```



* Board List부분

![image-20200923173622915](C:\Users\mgk04.DESKTOP-8Q51H2D\AppData\Roaming\Typora\typora-user-images\image-20200923173622915.png)

```python
<urls.py>

urlpatterns = [
    path('index/', views.loginForm, name='loginForm'),
    path('registerForm/', views.registerForm, name='registerForm'),
    path('register/', views.register, name='register'),
    path('login/', views.login, name='login'),
    path('logout/', views.logout, name='logout'),
    path('bbs_list/', views.list, name='bbs_list'),
    path('bbs_registerForm/', views.bbsRegisterForm, name='bbs_registerForm'),
    path('bbs_register/', views.bbsRegister, name='bbs_register'),
    path('bbs_read/<int:id>', views.bbsRead, name='bbs_read'),
    path('bbs_remove/', views.bbsRemove, name='bbs_remove'),
    path('bbs_modifyForm/', views.bbsModifyForm, name = 'bbs_modifyForm'),
    path('bbs_modify/', views.bbsModify, name='bbs_modify'),
    path('bbs_search/', views.bbsSearch, name='bbs_search'),
]
```

```python
<views.py>

# ajax - json
def bbsSearch(request):
    print('------------ajax json bbsSearch')
    type = request.POST['type']
    keyword = request.POST['keyword']
    print("type:", type, "keyword:", keyword)

    # model
    # select * from table where subject like '%공지%'
    # -> modelName.objects.filter(subject_icontains='공지')

    # select * from table where subject like '공지%'
    # -> modelName.objects.filter(subject_startwith='공지')

    # select * from table where subject like '%공지'
    # -> modelName.objects.filter(subject_endwith='공지')

    if type == 'title':
        boards = Bbs.objects.filter(title__startswith=keyword)
    if type == 'writer':
        boards = Bbs.objects.filter(writer__startswith=keyword)
    print("a jax -- result:",boards)
    dict = {'test' : 'json_sample'}

    data = []
    for board in boards:
        data.append({
            'id' : board.id,
            'title' : board.title,
            'writer' : board.writer,
            'regdate' : board.regdate,
            'viewcnt' : board.viewcnt
        })
    return JsonResponse(data, safe=False)

```

