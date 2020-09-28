# Django 실습

목표 : 전반적인 게시판의 구현에 대해서 알아보자 !



###### GET과 POST 개념 차이 이해하기

사용자 입장에서 GET방식의 URL호출은 URL 뒤에 물음표(?)를 이용한 파라미터 값이 보인다. 하지만 POST 방식의 URL 호출에서는 파라미터 값을 body안에 넣어서 보내므로 사용자 입장에서 파라미터 값을 직접적으로 확인할 수 없다. 즉 URL 호출에서 파라미터 값 전달 방식의 차이가 존재한다. GET방식에서는 전송 할 수 있는 데이터의 형태나 크기의 제한이 있지만, POST 방식에서는 그렇지않고 일반적으로는 GET방식의 호출이 POST 방식의 호출보다 따른 속도를 가진다.



###### session에 id값 저장

```python
#views.py

def login(request) :
    if request.method == 'GET' :
        return redirect('login')
    elif request.method == 'POST' :
        id = request.POST['id']
        pwd = request.POST['pwd']

        # select * from table where id = 1 and pwd = 1;
        # -> modelName.objects.filter(id = 1, pwd = 1)

        # user = BbsUserRegister.objects.filter(user_id = id, user_pwd = pwd)       
        # filter : list 타입 return
        user = BbsUserRegister.objects.get(user_id = id, user_pwd = pwd)            
        # get : object 타입 return

        context = {}
        if user is not None :
            request.session['user_name'] = user.user_name     # 추가
            request.session['user_id'] = user.user_id
            context['name'] = request.session['user_name']
            context['id'] = request.session['user_id']  #keyvalue로 두개의 값이 심어짐 name id

        return render(request, 'home.html', context)
```

```python
def loginForm(request):
    if request.session.get('user_id'):
        context = {'id': request.session['user_id'], 'name': request.session['user_name']}
        return render(request, 'home.html', context)

    return render(request,'login.html')
    
def logout(request):
    request.session['user_name']={}
    request.session['user_id']={}
    request.session.modified = True
    return redirect('loginForm')
```



##### 게시판 기능 구현하기 

 ```python
# urls.py

urlpatterns = [
    path('index/', views.loginForm, name='loginForm'),
    path('registerForm/', views.registerForm, name='registerForm'),
    path('register/', views.register, name='register'),
    path('login/', views.login, name='login'),
    path('logout/', views.logout, name='logout'),
    path('bbs_list/', views.list, name='bbs_list'),
    path('bbs_registerForm/', views.bbsRegisterForm, name='bbs_registerForm'),]
 ```

```python
# views.py

def bbsRegisterForm(request):
    context = {'name': request.session['user_name'], 'id': request.session['user_id']}
    return render(request,'bbsRegisterForm.html',context)

- render( ,templates(html),context) - forward 
context에 데이터를 심으면 해당 데이터는 요청된 페이지 내에서만 사용이 가능한 scope 가지게된다
- redirect(새로운 request url 요청할수있게된다)
```

```python
# bbsRegisterForm.html
# - html (tag + text)
# - {{print}}
# - {% 동적 코드를 작성하고자 할 때 %}
# - {% 프리젠테이션 레이어에 로직을 심을 수 있다 %}


{% include 'header.html' %}
{% block content %}
.
.

{% endblock %}
{% include 'footer.html' %}
```



##### 테이블 값 가져오기

```python
# urls.py

urlpatterns = [
    path('index/', views.loginForm, name='loginForm'),
    path('registerForm/', views.registerForm, name='registerForm'),
    path('register/', views.register, name='register'),
    path('login/', views.login, name='login'),
    path('logout/', views.logout, name='logout'),
    path('bbs_list/', views.list, name='bbs_list'),
    path('bbs_registerForm/', views.bbsRegisterForm, name='bbs_registerForm'),
    path('bbs_register/', views.bbsRegister, name='bbs_register'),]
```

```python
# views.py

def bbsRegister(request):
    if request.method =='GET':
        return redirect('bbs_registerForm')
    elif request.method == "POST":
        title=request.POST['title']
        content = request.POST['content']
        writer = request.POST['writer']

        board = Bbs(title=title, content=content, writer=writer)
        board.save()

        return redirect('bbs_list')
    #return render(request,'list.html') # 방금 입력했던 글에 대한 정보를 못가져옴
```

```python
# read.html

{% include 'header.html' %}
{% block content %}
.
. 
{% endblock %}
{% include 'footer.html' %}
```



##### 게시글 확인 및 수정

```python
# urls.py

urlpatterns = [
    path('index/', views.loginForm, name='loginForm'),
    path('registerForm/', views.registerForm, name='registerForm'),
    path('register/', views.register, name='register'),
    path('login/', views.login, name='login'),
    path('logout/', views.logout, name='logout'),
    path('bbs_list/', views.list, name='bbs_list'),
    path('bbs_registerForm/', views.bbsRegisterForm, name='bbs_registerForm'),
    path('bbs_register/', views.bbsRegister, name='bbs_register'),
    path('bbs_read/<int:id>', views.bbsRead, name='bbs_read'),]
```

```python
# view.py 

def bbsRead(request,id):
    print('param-',id)
    # model 작업을 필요로 하게 된다.

    bbs = Bbs.objects.get(id=id)
    # viewcnt update
    bbs.viewcnt = bbs.viewcnt +1
    bbs.save()
    context = {'bbs': bbs,'name':request.session['user_name'],'id':request.session['user_id']}
    return render(request,'read.html',context) 
                                          #render함수는 Html 파일을 사용자에게 보여주고자한다
```



##### 게시판 목록으로 돌아가기

```python
# read.html

<script>
				
$(document).ready(function(){
	$('#listBtn').click(function(){
		location.href='../bbs_list';
	})

</script>
```



##### 게시글 삭제하기

```python
# read.html

<script>
				
$(document).ready(function(){
	$('#listBtn').click(function(){
		location.href='../bbs_list';
	})
	$('.btn-danger').click(function(){
		$('#removeFrm').attr('action','../bbs_remove/');
		$('#removeFrm').submit(); //$('#removeFrm')이것은 폼태그 / 폼태그에 submit를 추가해준다
	})
});

</script>
```

```python
urls.py

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
]
```

```python
def bbsRemove(request):
    id = request.POST['id']
    bbs = Bbs.objects.get(id=id)
    bbs.delete()
    return redirect('bbs_list')
```

![image-20200922171411579](C:\Users\mgk04.DESKTOP-8Q51H2D\AppData\Roaming\Typora\typora-user-images\image-20200922171411579.png)