#  Django 웹 만들기 (2)

* 모델을 통해 데이터를 가져오는 실습진행

* 모델을 만드는 방법에 대해서는 ORM의 개념을 통해 쉽게 만들수 있음 class 만들어서 함수 선언해주면 자동으로 table이 만들어짐

* 템플릿이라는것은 화면을 담당하는 html들이 있는 영역

* 그것을 중간에서 control하는 것이 View이다

* View는 함수를 가지고 있고 그 안에서 로직 처리가 이루어진다.

* 상황에 따라서는 모델과 통신할수도있고 단순히 화면의 역할을 할수 있다.

* 뷰가 실행되기 위해서는 사용자의 요청을 받아서 분석할 수 있는 URL이 필요하다



작업 진행

먼저 사용자의 request URL을 정리하고 사용자의 URL이 있으면 View에다가 함수를 정리하고 이 View안에서 모델과 통신해서 Template으로 보내는 형식 



### 1. 프로젝트 뼈대 만들기 

     ####       App 생성

       ```
python manage.py startapp PollsApp # PollsApp 앱생성
       ```

```python
# digangoWEB -> settings.py에 환경설정 진행

ALLOWED_HOSTS = ['127.0.0.1' , 'localhost']

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'helloApp',
    'PollsApp',                     # 등록된 앱에 대한 최초의 접근은 index로 하고싶다!
]
TIME_ZONE = 'Asia/Seoul'
```



###  2 . URLconf 코딩하기

```python
from django.contrib import admin
from django.urls import path, include
from PollsApp import views

urlpatterns = [
    path('index/', views.index, name = 'index'),
    path('<int:question_id>/', views.choice, name = 'choice'),
    path('vote/', views.vote, name='vote'),
    path('result/', views.result, name = 'result'),
]
```



### 3. 뷰 코딩하기

```python
from django.shortcuts import render,get_object_or_404, redirect
from django.http import HttpResponse,HttpResponseRedirect
from django.urls import reverse

# .models로부터 모든것을 가져오겠다

# Create your views here.
from .models import *
def index(request):                  # View에서 index라는 함수 생성 !
    # view에서 일어나는 작업 -토신
    # select * from table
    # -> modelName.objects.all()

    # select * from table where id=1;
    # -> modelName.objects.filter(id=1)

    # and 조건
    # select * from table where (id=1 and pwd=1);
    # -> modelName.objects.filter(id=1 and pwd=1)

    # or 조건
    # select * from table where id =1 or pwd =1;
    # -> modelName.objects.filter(Q(id=1)/Q(pwd=1))

    # select * from table where subject like '%공지%'
    # -> modelName.objects.filter(subject_icontains='공지')

    # select * from table where subject like '공지%'
    # -> modelName.objects.filter(subject_startwith='공지')

    # select * from table where subject like '%공지'
    # -> modelName.objects.filter(subject_endwith='공지')

    # insert into table values('')
    # model(attr=value,attr=value .....)
    # -> model.save()

    # delete * from table where id=1
    # -> modelName.objects.get(id=1).delete()

    # update table set attr = value where id=1
    # obj =model.Name.objects.get(id=1)         # 데이터 하나꺼내오기
    # obj.attr='변경'
    # obj.save() -- commit

    lists = Question.objects.all()              # 모델과 통신하는작업
    context = {'lists' : lists}                 # 모델과 통신하는 작업
    
    return render(request,'polls/index.html', context) 
                                      #templates로 이동할때 데이터를 가지고 이동하고 싶었음 
    # return HttpResponse("테스트 링크~ 잘되나요?")
#GET방식
def choice(request,question_id): 
    print('param question_id',str(question_id))
    lists = get_object_or_404(Question,pk=question_id)
    print("-"*100)
    print(lists)
    print("-"*100)
    context={'clist':lists}
    return render(request,"polls/choice.html",context)

def vote(request):
    context = {}
    print(request)
    choice = request.POST['choice'] # name 값을 받는다. 이 name 안에는 value 가 담겨있다.
    question_id = request.POST['question_id'] # name 값을 받는다. 이 name 안에는 value 가 담겨있다.
    print(choice)
    print(question_id)

    question = get_object_or_404(Question, pk=question_id) # 선택된 question
    checked_choice = question.choice_set.get(pk=choice) # 선택된 초이스 이건 부모 자식간의 관계가 있을 때 가능하다.
    checked_choice.votes += 1 #
    checked_choice.save()

    context = {}
    request.session['question_id']  = question_id
    return redirect('result')
    # return HttpResponseRedirect(reverse('polls:result', args=(question.id,)))
    # return render(request, 'polls/result.html', context)

def result(request) :
    question_id = request.session['question_id']
    print('--------------------- views.result', str(question_id))
    question = get_object_or_404(Question,pk=question_id)
    context = {'question':question}
    return render(request, 'polls/result.html', context)
```

* 사용자가 index를 쳤을때  (서버를 실행 시키면 python  manage.py runserver) 페이지 생성

  내가 지금 화면을 보고있는 것은 client의 입장

  클릭했을때 서버에서 동작했을때는 서버 개발자의 입장으로 봐야함

```

from django.contrib import admin
from django.urls import path, include
from PollsApp import views

urlpatterns = [
    path('index/', views.index, name = 'index'),
    path('<int:question_id>/', views.choice, name = 'choice'),
    path('vote/', views.vote, name='vote'),
    path('result/', views.result, name = 'result'),
]
```

### 4. 템플릿 코딩하기

```python
[templates -> choice.html]

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1>{{clist.question_text}}</h1>
    <hr/>
    <form method="post" action="{% url 'vote' %}">
    <input type="hidden" name="question_id" value="{{clist.id}}"> <!-- 이런식으로 hidden으로 형태는 안보이게 하되 값은 넣어서 보내준다. -->
        {% csrf_token%} <!-- django 에서 post를 쓸때는 csrf 토큰을 사용한다. 보안을 위해서 이다. -->
        {% for  choice in clist.choice_set.all%}<!--//  xxx_set.all 은  템플릿쪽에서 사용하는 코드로 모든 객체들을 가져온다.  -->
    <input type="radio"
           name="choice"
           value="{{choice.id}}"> <!-- name 이라는 것이 변수 이름이다.-->
    <label>
        {{ choice.choice_text}}
    </label><br/>
    {% endfor %}
        <p/>
        <input type="submit" value="VOTE">
    </form>
</body>
</html>
```

```python
[templates->index.html]

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    {% if lists %}
    <ul>
        {% for question in lists %}
        <li><a href="../{{question.id}}">{{question.question_text}}</a></li>
        {% endfor %}
    </ul>
    {% else %}
        <p>데이터가 존재하지 않습니다.</p>
    {% endif %}
</body>
</html>
```

```python
[templates->result.html]

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1>{{ question.question_text }}</h1>
    <hr/>

    <ul>
        {% for choice in question.choice_set.all %}
        <li>{{choice.choice_text}} - {{choice.votes}}</li>
        {% endfor %}
    </ul>
    <p/>
    <a href="{% url 'index' %}">첫 페이지로 이동</a>

</body>
</html>
```



### 5. 모델 코딩하기

```python
from django.db import models

# Create your models here.


class Question(models.Model) :
    question_text = models.CharField(max_length = 200)
    regdate = models.DateTimeField('date published')

    def __str__(self):
        return self.question_text + " , " + str(self.regdate)


class Choice(models.Model) :
    question = models.ForeignKey(Question, on_delete = models.CASCADE)
    choice_text = models.CharField(max_length = 200)
    votes = models.IntegerField(default = 0)

    def __str__(self):
        return str(self.question) + " , " + self.choice_text + " , " + str(self.votes)
```

```
from django.contrib import admin
from .models import *
# Register your models here.
admin.site.register(Question)
admin.site.register(Choice)
```

![image-20200919024446929](C:\Users\mgk04.DESKTOP-8Q51H2D\AppData\Roaming\Typora\typora-user-images\image-20200919024446929.png)

![image-20200919025900157](C:\Users\mgk04.DESKTOP-8Q51H2D\AppData\Roaming\Typora\typora-user-images\image-20200919025900157.png)

![image-20200919025923743](C:\Users\mgk04.DESKTOP-8Q51H2D\AppData\Roaming\Typora\typora-user-images\image-20200919025923743.png)