# 웹 프레임 워크 Django

Model 안전하게 데이터를 저장

View 데이터를 적절하게 유저에게 보여줌

Templete 사용자 입력과 이벤트에 반응하여 Model과 View를 업데이트 !

![image-20200921012300950](C:\Users\mgk04.DESKTOP-8Q51H2D\AppData\Roaming\Typora\typora-user-images\image-20200921012300950.png)

* 프로젝트 생성

  ```
  django-admin startproject ****
  ```

* app 생성

  ```
  ./manage.py startapp *****
  ```

### settings.py

* DEBUD : 디버그 모드 설정
* INSTALLED_APPS : pip로 설치한 앱 또는 본인이 만든 app을 추가
* MIDDELWARE_CLASSES : request와 response 사이의 주요 기능 레이어
* DATABASES : 데이터베이스 엔진의 연결 설정
* STATIC_URL : 정적 파일의 URL(css,javascript,image,etc.)



### manage.py

주요 명령어

* startapp-앱생성
* runserver-서버실행
* creatsuperuser-관리자 생성
* makemigrations app-app의 모델 변경 사항 체크
* migrate-변경사항을 DB에 반영
* shell-쉘을 통해 데이터를 확인
* collectstatic-static 파일을 한곳에 모음



# 웹 페이지 만들기

* BbsApp 앱 생성

```
python manage.py startapp  BbsApp
```



* djangoWEB ->  settings.py

  * app 추가

    ```python
    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'helloApp',
        'PollsApp',
        'BbsApp',          #BbsApp
    ]
    ```

  * 경로등록

     ```
    from django.contrib import admin
    from django.urls import path,include
    
    urlpatterns = [
        path('admin/', admin.site.urls),
        path('hello/', include('helloApp.urls')),
        path('polls/', include('PollsApp.urls')),
        path('bbs/',include('BbsApp.urls')), #path에 bbs 추가
    ]
    ```

    

  * 자바스크립트, css등을 사용하는 directory 설정

    ```python
    STATIC_URL = '/static/'
    STATICFILES_DIRS = [os.path.join(BASE_DIR, 'BbsApp', 'static')]
    STATIC_ROOT = os.path.join(BASE_DIR, 'static')
    ```

    

* djangoWEB -> BbsApp->templates-> urls.py

  ```
  from django.contrib import admin
  from django.urls import path,include
  from BbsApp import views
  
  urlpatterns = [
      path('index/', views.loginForm, name='loginForm'),
      path('registerForm/', views.registerForm, name='registerForm'),
  ]
  ```

   path('registerForm/', views.registerForm, name='registerForm')에서

  **'registerForm/'** => URL상에서 보여지는 path경로

  **views.registerForm** =>  함수 이름

  **name='registerForm'**=> 개발자가 path를 찾는 이름

```
from django.shortcuts import render, redirect
from django.http import HttpResponse
from .models import *

# Create your views here.
def loginForm(request):
    return render(request,'login.html')

def registerForm(request):
    return render(request,'join.html')
```

![image-20200921164738906](C:\Users\mgk04.DESKTOP-8Q51H2D\AppData\Roaming\Typora\typora-user-images\image-20200921164738906.png)

models와 통신 

개발자 입장에서는 form에 저장되어있는 id pwd와 name을 DB에 저장시키는 작업 선행



* djangoWEB -> BbsApp->templates-> join.html

```
{% load static %}


<html>
<head>
<meta charset="UTF-8">
<title>AdminLTE 2 | Log in</title>
<meta
	content='width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no'
	name='viewport'>
<!-- Bootstrap 3.3.4 -->
<link href="{% static '/resources/bootstrap/css/bootstrap.min.css' %}" rel="stylesheet"
	type="text/css" />
<!-- Font Awesome Icons -->
<link
	href="https://maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css"
	rel="stylesheet" type="text/css" />
<!-- Theme style -->
<link href="{% static '/resources/dist/css/AdminLTE.min.css' %}" rel="stylesheet"
	type="text/css" />
<!-- iCheck -->
<link href="{% static '/resources/plugins/iCheck/square/blue.css' %}" rel="stylesheet"
	type="text/css" />

<!-- HTML5 Shim and Respond.js IE8 support of HTML5 elements and media queries -->
<!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
<!--[if lt IE 9]>
        <script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script>
        <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
    <![endif]-->
</head>
<body class="login-page">
	<div class="login-box">
		<div class="login-logo">
			<a href="/resources/index2.html"><b>SEMI-</b>Project</a>
		</div>
		<!-- /.login-logo -->
		<div class="login-box-body">
			<p class="login-box-msg">Sign in to start your session</p>

			  <form action="{% url 'register' %}" method="post">  #저장하는 방식이 POST방식
				{% csrf_token %}
				
				<div class="form-group has-feedback">
					<input type="text" name="id" class="form-control"
						placeholder="USER ID" /> <span
						class="glyphicon glyphicon-envelope form-control-feedback"></span>
				</div>
				<div class="form-group has-feedback">
					<input type="password" name="pwd" class="form-control"
						placeholder="Password" /> <span
						class="glyphicon glyphicon-lock form-control-feedback"></span>
				</div>
				<div class="form-group has-feedback">
					<input type="text" name="name" class="form-control"
						placeholder="Name" /> 
					<span class="glyphicon glyphicon-user form-control-feedback"></span>
				</div>
				
				
				<div class="row">
			    <div class="col-xs-12">
			      <button type="submit" class="btn btn-primary btn-block">Register</button>
			    </div><!-- /.col -->
			  </div>
			</form>
			
		</div>
		<!-- /.login-box-body -->
	</div>
	<!-- /.login-box -->

	<!-- jQuery 2.1.4 -->
	<script src="{% static  '/resources/plugins/jQuery/jQuery-2.1.4.min.js' %}"></script>
	<!-- Bootstrap 3.3.2 JS -->
	<script src="{% static '/resources/bootstrap/js/bootstrap.min.js' %}"
		type="text/javascript"></script>
	<!-- iCheck -->
	<script src="{% static '/resources/plugins/iCheck/icheck.min.js' %}"
		type="text/javascript"></script>
	<script>
      $(function () {
        $('input').iCheck({
          checkboxClass: 'icheckbox_square-blue',
          radioClass: 'iradio_square-blue',
          increaseArea: '20%' // optional
        });
      });
    </script>
</body>
</html>
```

```
# djangoWEB -> BbsApp->templates-> urls.py

from django.contrib import admin
from django.urls import path,include
from BbsApp import views

urlpatterns = [
    path('index/', views.loginForm, name='loginForm'),
    path('registerForm/', views.registerForm, name='registerForm'),
    path('register/', views.register, name='register'),
]
```

```
# djangoWEB -> BbsApp->templates-> views.py
뷰에서 모델과 통신하는 작업

from django.shortcuts import render, redirect
from django.http import HttpResponse
from .models import *

# Create your views here.
def loginForm(request):
    return render(request,'login.html')

def registerForm(request):
    return render(request,'join.html')

```

* djangoWEB -> BbsApp->templates-> model.py

  model을 상속 받음

  ```
  from django.db import models
  from django.utils import timezone
  # Create your models here.
  
  class BbsUserRegister(models.Model):
      user_id = models.CharField(max_length=50) #컬럼의 타입이 caracter을 담음
      user_pwd = models.CharField(max_length=50) #user_pwd 컬럼 이름
      user_name = models.CharField(max_length=50)
  
      def __str__(self):                      #디버그 코드 str-> 내장함수
          return  self.user_id+","+self.user_pwd+","+ self.user_name
  ```



* model을   디비(테이블) 만드는 명령어

```
python manage.py makemigrations #테이블 만드는것
python manage.py migrate # DB에 들어가서 테이블이 만들어졌는지등을 확인할때 계정이 만들어졌는지 확인
```

* djangoWEB -> BbsApp->templates-> admin.py

```
from django.contrib import admin
from .models import *

# Register your models here.
admin.site.register(BbsUserRegister)
```



* ##### 계정을 등록시키는 작업(회원가입) 

```
{% load static %}

<html>
  <head>
    <meta charset="UTF-8">
    <title>AdminLTE 2 | Log in</title>
    <meta content='width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no' name='viewport'>
    <!-- Bootstrap 3.3.4 -->
    <link href="{% static '/resources/bootstrap/css/bootstrap.min.css'%}" rel="stylesheet" type="text/css" />
    <!-- Font Awesome Icons -->
    <link href="https://maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css" rel="stylesheet" type="text/css" />
    <!-- Theme style -->
    <link href="{% static '/resources/dist/css/AdminLTE.min.css' %}" rel="stylesheet" type="text/css" />
    <!-- iCheck -->
    <link href="{% static '/resources/plugins/iCheck/square/blue.css' %}" rel="stylesheet" type="text/css" />

  </head>
  <body class="login-page">
    <div class="login-box">
      <div class="login-logo">
        <a href="/resources/index2.html"><b>SEMI-</b>Project</a>
      </div><!-- /.login-logo -->
      <div class="login-box-body">
        <p class="login-box-msg">Sign in to start your session</p>

<form action="{% url 'login' %}" method="post">
  {% csrf_token %}
  <div class="form-group has-feedback">
    <input type="text" name="id" class="form-control" placeholder="USER ID"/>
    <span class="glyphicon glyphicon-envelope form-control-feedback"></span>
  </div>
  <div class="form-group has-feedback">
    <input type="password" name="pwd" class="form-control" placeholder="Password"/>
    <span class="glyphicon glyphicon-lock form-control-feedback"></span>
  </div>
  <div class="row">
    <div class="col-xs-8">    
      <div class="checkbox icheck">
        <label>
          <input type="checkbox" name="useCookie"> Remember Me
        </label>
      </div>                        
    </div><!-- /.col -->
    <div class="col-xs-4">
      <button type="submit" class="btn btn-primary btn-block btn-flat">Sign In</button>
    </div><!-- /.col -->
  </div>
</form>


        <a href="#">I forgot my password</a><br>
        <a href="{% url 'registerForm' %}" class="text-center">Register a new membership</a>               # %는 장고에서 지원하고있는 템플릿 태그들

      </div><!-- /.login-box-body -->
    </div><!-- /.login-box -->

    <!-- jQuery 2.1.4 -->
    <script src="{% static '/resources/plugins/jQuery/jQuery-2.1.4.min.js' %}"></script>
    <!-- Bootstrap 3.3.2 JS -->
    <script src="{% static '/resources/bootstrap/js/bootstrap.min.js' %}" type="text/javascript"></script>
    <!-- iCheck -->
    <script src="{% static '/resources/plugins/iCheck/icheck.min.js' %}" type="text/javascript"></script>
    <script>
      $(function () {
        $('input').iCheck({
          checkboxClass: 'icheckbox_square-blue',
          radioClass: 'iradio_square-blue',
          increaseArea: '20%' // optional
        });
      });
    </script>
  </body>
</html>

```

**% 는 장고에서 지원하고있는 템플릿 태그들**

{% 동적 코드를 작성하고자 할 때 %}

{% 프리젠테이션 레이어에 로직을 심을 수 있다 %}



*  djangoWEB -> BbsApp->templates-> views.py

  ```
  from django.shortcuts import render, redirect
  from django.http import HttpResponse
  from .models import *
  
  # Create your views here.
  def loginForm(request):
      return render(request,'login.html')
  
  def registerForm(request):
      return render(request,'join.html')
  
  def register(request):
      if request.method=='Post':
          id   = request.Post['id']
          pwd  = request.Post['pwd']
          name = request.Post['name']
          
          register = BbsUserRegister(user_id=id, user_pwd=pwd, user_name=name)
          register.save()  #insert가 이루어짐
      return redirect('loginForm') # redirect(새로운 request url 요청할수있게된다)
  ```

  어디로 이동할까?뷰에서 모델과 통신해서 insert시킴 그럼 다시 templates로 이동

  로그인 되는 화면으로 이동시킬것.

  

  return redirect('loginForm') 이라고 쓴 이유는 사용자가 치고들어온 index를 찾아서  loginFoem 함수를 실행

* views.py

  HttpResponse(x)
  render( ,templates(html),context) - forward
  context에 데이터를 심으면 해당 데이터는 요청된 페이지 내에서만
  사용이 가능한 scope 가지게된다
  session에 심어서 데이터 사용 범위를 모든 템플릿에서 사용할수있는 데이터로 저장해야한다.



* ##### 홈 화면

  ```python
  urlpatterns = [
      path('index/', views.loginForm, name='loginForm'),
      path('registerForm/', views.registerForm, name='registerForm'),
      path('register/', views.register, name='register'),
      path('login/', views.login, name='login'),
      ]
  ```

*  djangoWEB -> BbsApp->templates-> view.py

```python
def login(request) :
    if request.method == 'GET' :
        return redirect('login')
    elif request.method == 'POST' :
        id = request.POST['id']
        pwd = request.POST['pwd']

        # select * from table where id = 1 and pwd = 1;
        # -> modelName.objects.filter(id = 1, pwd = 1)

        # user = BbsUserRegister.objects.filter(user_id = id, user_pwd = pwd)       # filter : list 타입 return
        user = BbsUserRegister.objects.get(user_id = id, user_pwd = pwd)            # get : object 타입 return

        context = {}
        if user is not None :
            request.session['user_name'] = user.user_name
            context['userSession'] = request.session['user_name']
        # context에 데이터를 심으면 해당 데이터는 요청된 페이지 내에서만
        # 사용이 가능한 scope 가지게된다
        # session에 심어서 데이터 사용 범위를 모든 템플릿에서 사용할수있는 데이터로 저장해야한다.
        return render(request, 'home.html', context)
```

*  djangoWEB -> BbsApp->templates-> home.html

```python
{% include 'header.html' %}
{% block content %}
.
.
{% endblock %}
{% include 'footer.html' %}
```

* ##### 로그아웃

```python
# djangoWEB -> BbsApp->templates-> urls.py
urlpatterns = [
    path('index/', views.loginForm, name='loginForm'),
    path('registerForm/', views.registerForm, name='registerForm'),
    path('register/', views.register, name='register'),
    path('login/', views.login, name='login'),
    path('logout/', views.logout, name='logout'),
    ]
```

```python
# djangoWEB -> BbsApp->templates-> view.py
def logout(requset):
    requset.session['user_name']={}
    requset.session.modified = True
    return redirect('loginForm')
```



* 게시판

```python
# djangoWEB -> BbsApp->templates-> models.py
# Bbs 객체 생성
class Bbs(models.Model):
    # id =models.AutoField(primary key= True)
    title = models.CharField(max_length=100)
    writer = models.CharField(max_length=100)
    content = models.TextField()
    regdate = models.DateTimeField(default=timezone.now())
    viewcnt = models.IntegerField(default=0)

    def __str__(self):
        return self.title
```

```python
# djangoWEB -> BbsApp->templates-> admin.py
from django.contrib import admin
from .models import *

# Register your models here.
admin.site.register(BbsUserRegister)
admin.site.register(Bbs)
```

```
Bbs -> 테이블로 변환
python manage.py makemigrations -> 테이블 만드는것 
python manage.py migrate  ->DB에 들어가서 테이블이 만들어졌는지등을 확인할때 계정이 만들어졌는지 확인
```



```python
# djangoWEB -> BbsApp->templates-> urls.py

from django.contrib import admin
from django.urls import path,include
from BbsApp import views

urlpatterns = [
    path('index/', views.loginForm, name='loginForm'),
    path('registerForm/', views.registerForm, name='registerForm'),
    path('register/', views.register, name='register'),
    path('login/', views.login, name='login'),
    path('logout/', views.logout, name='logout'),
    path('bbs_list/', views.list, name='bbs_list'),
]
```

```python
# djangoWEB -> BbsApp->templates-> views.py

def list(requset):
    # select * from table;
    # -> modelName.objects.all()
    boards = Bbs.objects.all()
    print('boards result-', type(boards), boards)
    context = {'boards': boards}
    return render(requset, 'list.html', context)
```

```
# djangoWEB -> BbsApp->templates-> list.html

{% include 'header.html' %}
{% block content %}
.
.
{% endblock %}
{% include 'footer.html' %}
```

* 서버실생

```
python manage.py runserver
```

![image-20200921205841635](C:\Users\mgk04.DESKTOP-8Q51H2D\AppData\Roaming\Typora\typora-user-images\image-20200921205841635.png)

