# do it ! 점프 투 파이썬 

### 04장 파일 읽고 쓰기

#####  파일 생성하기

```python
f = open("새파일.txt",'w')
```

```
파일객체 = open(파일이름, 파일 열기모드)
```

| 파일 열기 모드 | 설명                                                       |
| -------------- | ---------------------------------------------------------- |
| r              | 읽기 모드 - 파일을 읽기만 할 때 사용                       |
| w              | 쓰기 모드 - 파일에 내용을 쓸 때 사용                       |
| a              | 추가 모드  - 파일의 마지막에 새로운 내용을 추가 할 때 사용 |

만약 새파일.txt을 C:/doit 디렉터리에 생성하고 싶다면 다음과 같이 작성

```python
f = open("C:/doit/새파일.txt",'w')
```

![image-20200920153224080](C:\Users\mgk04.DESKTOP-8Q51H2D\DOIT\jumpto1.assets\image-20200920153224080.png)

C:/doit에 새파일이 추가된것을 확인 할 수 있다.



Q. 복습.txt파일을 C:/doit 디렉터리에 만들어보자.

```python
f = open("C:/doit/복습.txt",'w')
```

![image-20200920153432930](C:\Users\mgk04.DESKTOP-8Q51H2D\DOIT\jumpto1.assets\image-20200920153432930.png)

복습.txt가 추가된것을 확인 할 수있디.

##### 파일을 쓰기 모드로 열어 출력값 적기

```python
f = open("C:/doit/새파일.txt",'w')
for i in range(1,11):
    data="%d번째 줄입니다.\n" % i
    f.write(data)
f.close()
```

![image-20200920153709965](C:\Users\mgk04.DESKTOP-8Q51H2D\DOIT\jumpto1.assets\image-20200920153709965.png)

위 프로그램을 다른 프로그램과 비교해보자.

```python
f = open("C:/doit/새파일.txt",'w')
for i in range(1,11):
    data="%d번째 줄입니다.\n" % i
    print(data)
```

두 프로그램의 차이점은 data를 출력하는 방법이다. 두번째 방법은 우리가 계속 사용해 왔던 모니터 화면에 출력하는 방법이다. 첫번째 방법은 모니터 화면 대신 파일에 결과값을 적는 방법이다.

![image-20200920154010744](C:\Users\mgk04.DESKTOP-8Q51H2D\DOIT\jumpto1.assets\image-20200920154010744.png)



##### 프로그램 외부에 저장된 파일을 읽는 여러가지 방법

* readline 함수 사용하기

  ```python
  f = open("C:/doit/새파일.txt",'r')
  line=f.readline()
  print(line)
  ```

  ![image-20200920154405289](C:\Users\mgk04.DESKTOP-8Q51H2D\DOIT\jumpto1.assets\image-20200920154405289.png)

   만약 모든 줄을 읽어서 화면에 출력하고 싶다면 다음과 같이 작성하면 된다.

  ```python
  f = open("C:/doit/새파일.txt",'r')
  while True:
      line=f.readline()
      if not line: break
      print(line)
  f.close()
  ```

  ![image-20200920154716885](C:\Users\mgk04.DESKTOP-8Q51H2D\DOIT\jumpto1.assets\image-20200920154716885.png)



* readlines함수 사용하기

  ```python
  f=open("C:/doit/새파일.txt",'r')
  lines=f.readlines()
  for line in lines:
      print(line)
  f.close()
  ```

* read 함수 이용하기

  ```python
  f=open("C:/doit/새파일.txt",'r')
  data=f.read()
  print(data)
  ```



##### 파일에 새로운 내용 추가하기

쓰기모드('w')로 파일을 열 때 이미 존재하는 파일을 열면 그 파일의 내용이 모두 사라지게 된다. 하지만 원래 있던 값을 유지하면서 단지 새로운 값만 추가해야 할 경우도 있다. 이러경우 파일을 추가모드('a')로 열면된다.

````python
f=open("C:/doit/새파일.txt",'a')
for i in range(11,20):
    data="%d번째 줄입니다\n" %i
    f.write(data)
f.close()
print(f)
````

![image-20200920155529358](C:\Users\mgk04.DESKTOP-8Q51H2D\DOIT\jumpto1.assets\image-20200920155529358.png)

##### with문과 함께 사용하기

지금까지 살펴본 예제를 보면 항상 다음과 같은 방식으로 파일을 열고 닫아왔다.

```python
f = open("foo.txt", "w")
f.write("Life is too short, you need python")
f.close()
```

```python
with open("foo.txt","w") as f:
    f.write("Life is too short,you need python")
```

with문을 사용하면 with 블록을 벗어나는 순간 열린 파일 객체 f가 자동으로 close되어 편리하다.



### 05장 클래스

#### 클래스는 왜 필요한가?

```python
result1=0
result2=0

def add1(num):
    global result1
    result1+=num
    return  result1

def add2(num) :
    global  result2
    result2+=num
    return  result2

print(add1(3))
> 3
print(add1(5))
> 8
print(add2(2))
> 2
print(add2(3))
> 5
```

똑같은 일을 하는 add1과 add2 함수를 만들었고 각 함수에서 계산한 결과값을 유지하면서 저장하는 전역변수 result1,result2가 필요하게 되었다

계산기 1의 결과값이 계산기 2에 아무 영향을 끼치지 않음을 확인할 수 있다. 하지만 계산기 3개,5개,10개가 점점 더 많이 필요해진다면 어떻게 해야할까? 그때마다 전역 변수와 함수를 추가할 것인가? 여기에 빼기나 곱하기 등의 기능을 추가해야한다면 상황은 점점 더 어려워질것이다.



아직 클래스에 대해 배우지 않았지만, 위와 같은 경우에 클래스를 사용하면 다음과 같이 간단하게 해결 할 수 있다.

```python
class Calculator:
    def __init__(self):
        self.result = 0

    def add(self, num):
        self.result += num
        return  self.result
    def sub(self.num):
        self.result -= num
        return self.result

cal1 = Calculator()
cal2 = Calculator()

print(cal1.add(3))
> 3
print(cal1.add(5))
> 8
print(cal2.add(2))
> 2
print(cal2.add(3))
> 5
```

Calculator 클래스로 만든 별개의 계산기 cal1,cal2(파이썬에서 이것을 **객체** 라고 부른다)가 각각의 역할을 수행하낟. 그리고 계산기(cal1,cal2)의 결과값 역시 다른 계산기의 결과값과 상관없이 독립적인 값을 유지한다. 클래스를 사용하면 계산기 대수가 늘어나더라도 객체를 생성만 하면 되기 때문에 함수를 사용하는 경우와 달리 매우 간단해진다. 만약 빼기 기능을 추가하려면 Calculator 클래스에 다음과 같은 빼기 기능 함수를 추가해 주면 된다. (위에 추가함)



##### 클래스와 객체

* 클래스(class)  : 똑같은 무엇인가를 계속해서 만들어 낼수 있는 설계도면(과자 틀)
* 객체란(object) :  클래스 만든 피조물(과자 틀을 사용해 만든 과자) 
  * 객체마다 고유한 성격을 가진다 
  * 동일한 클래스로 만든 객체들은 서로 전혀 영향을 주지 않는다



파이썬 클래스의 가장 간단한 예

```python
class Cookie:
    pass

a=Cookie()
b=Cookie()
```

Cookie()의 결과값을 돌려받은 a와 b가 바로 객체이다. 마치 함수를 사용해서 그 결과값을 돌려받는 모습과 비슷하다.



#### 객체와 인스턴스의 차이

클래스로 만든 객체를 인스턴스라고 한다. 그렇다면 객체와 인스턴스의 차이는 무엇일까? a=Cookie() 이렇게 만든 a는 객체이다 a객체는 Cookie의 인스턴스이다. 즉 인스턴스라는 말은 특정 객체(a)가 어떤 클래스(Cookie)의 객체인지를 관계 위주로 설명할 때 사용한다. 'a는 인스턴스'보다는  'a의 객체' 라는 표현이 어울리며 'a는 Cookie의 객체'보다는 'a는 Cookie의 객체'보다는 'a는 Cookie의 인스턴스'라는 표현이 훨씬 잘 어울린다.



#### 사칙연산 클래스 만들기

* 클래스 구조 만들기

```python
class FourCal:
    pass
```

우선 대화형 인터프리터에서 pass란 문장만을 포함한 FourCal 클래스를 만든다. 현재에서 FourCal 클래스는 아무 변수나 함수도 포함하지 않지만 우리가 원하는 객체 a를 만들수 있는 기능은 가지고 있다.

```python
a=FourCal()
print(type(a))
> <class '__main__.FourCal'>
```

a=FourCal()로 a객체를 먼저 만들고 그 다음에 type(a)로 a객체가 어떤 타입인지를 알아보았다. 역시 객체 a가 FourCal 클래스의 객체임을 알 수 있다.



* 객체에 숫자 지정 할 수 있게 만들기

하지만 생성된 객체 a는 아무런 기능도 하지 못한다. 이제 더하기,나누기,곱하기,빼기 등의 기능을 하는 객체를 만들어야한다. 그런데 이러한 기능을 갖춘 객체를 만드려면 우선 a객체에 사칙연산을 할때 사용할 2개의 숫자를 먼저 알려주어야 한다.

```
def 함수 이름(매개변수):
	수행할 문장
```

클래스 안에 구현된 함수를 메서드(Method)라고 부른다.  클래스 내부의 함수는 항상 메서드라고 할것이다.

```python
class FourCal:
    def setdata(self,first,second): # 매서드의 매개변수
        self.first = first         # 매서드의 수행문
        self.second = second
```

 1) setdata 메서드의 매개변수

setdata 메서드는 매개변수로 self,first,second 3개의 입력값을 받는다. 그런데 일반 함수와 달리 메서드의 첫번째 매개변수 self는 특별한 의미를 가진다.

다음과 같이 a 객체를 만들고 a 객체를 통해 setdata 메서드를 호출해보자

```python
a=FourCal()
a.setdata(4,2)
```

setdata 메서드는 self,first,scond 총 3개의 매개변수가 필요한데 실제로 a.setdata(4,2)처럼 2개의 값만 전달했다. 왜 그럴까? 그 이유는 a.setdata(4,2)처럼 호출하면 setdata 메서드의 첫번째 매개변수 self에는 setdata메서드를 호출한 객체 a가 자동으로 전달되기 때문이다.

파이썬 메서드의 첫 번째 매개변수 이름은 관례적으로 self를 사용  객체를 호출할 때 호출한 객체 자신이 전달 되기 때문에  self를 사용한 것이다.



2) setdata메서드의 수행문

```python
class FourCal:
    def setdata(self,first,second): # 매서드의 매개변수
        self.first = first         # 매서드의 수행문
        self.second = second
        a=FourCal()
a.setdata(4,2)  
print(a.first)
> 4
print(a.second)
> 2
```

* a.setdata(4,2)처럼 호출하면 setdata 메서드의 매개변수 first,second에는 각각 값 4와 2가 전달되어 setdata메서드의 수행문은 다음과 같이 해석된다 

a,b 객체 만들기

```python
a.setdata(4,2)
print(a.first) # a 객체의 first를 다음과 같이 생성한다.
> 4
b.setdata(3,7) 
print(b.first) # b 객체의 frist를 다음과 같이 생성한다.
> 3
```

위와 같이 진행하면 b객체의 객체 변수 first 값 3이 저장된다는 것을 확인할 수 잇다.

그렇다면 a 객체의 first는 3으로 변할까? 기존 값을 유지할까?

```python
print(a.first)
> 4
```

a의 객체의 first 값은 b 객체의 first 값에 영향받지않고 원래 값을 유지하고 있음을 확인 가능

**클래스로 만든 객체의 객체변수는 다른 객체의 객체변수에 상관없이 독립적인 값을 유지 **



id 함수를 사용하면 객체변수가 독립적인 값을 유지한다는 점을 좀 더 명확하게 증명가능

```python
a=FourCal()
b=FourCal()
a.setdata(4,2)
b.setdata(3,7)
print(id(a.first))
> 1473408160
print(id(b.first))
> 1473408128
```

a 객체의first 주소값과 b 객체의 first 주소 값이 서로 다르므로 각각 다른 곳에 그값이 저장된다는 것을 알 수 있다 객체변수는 고유 값을 저장할 수 있는 공간이다. *객체 변수는 다른객체들 영향을 받지않고 독립적으로 그 값을 유지한다는점*  꼭 기억하자!

---

현재까지 완성된 FourCal 클래스

```python
class FourCal:
    def setdata(self,first,second): # 매서드의 매개변수
        self.first = first         # 매서드의 수행문
        self.second = second
```



* 더하기 기능 만들기

```python
class FourCal:
    def setdata(self,first,second): # 매서드의 매개변수
        self.first = first         # 매서드의 수행문
        self.second = second
    def add(self): # add메서드의 매개변수는 self이고 반환값을 result이다.
        result=self.first+self.second
        return  result # 해석 : result=4+2
a=FourCal() # a라는 객체의 first,second 객체변수에는 각각 값 4와 2가 저장
a.setdata(4,2)

print(a.add()) # a.add()라고 호출하면 add매세드가 호출되어 값 6이 출력될것
```

* 더하기 뺴기 곱하기 나누기 기능 만들기

```python
class FourCal:
    def setdata(self,first,second): # 매서드의 매개변수
        self.first = first         # 매서드의 수행문
        self.second = second
    def add(self): # add메서드의 매개변수는 self이고 반환값을 result이다.
        result=self.first+self.second
        return  result # 해석 : result=4+2
    def sub(self):
        result=self.first-self.second
        return  result
    def mul(self):
        result=self.first*self.second
        return  result
    def div(self):
        result=self.first/self.second
        return  result
a=FourCal() # a라는 객체의 first,second 객체변수에는 각각 값 4와 2가 저장
b=FourCal()
a.setdata(4,2)
b.setdata(100,50)

print(a.add()) # a.add()라고 호출하면 add매세드가 호출되어 값 6이 출력될것
> 6
print(b.add())
> 150
print(a.sub())
> 2
print(b.sub())
> 50
print(a.mul())
> 8
print(b.mul())
> 5000
print(a.div())
> 2.0
print(b.div())
> 2.0
```



###### 생성자(Constructor)

우리가 만든 FourCal 클래스를 다음과 같이 사용해보자

```python
a=FourCal()
a.add()
```

*AttributeError: 'FourCal' object has no attribute 'first'*

FourCal 클래스의 인스턴스 a에 setdata 메서드를 수행하지 않고 add 메서드를 수행하면 *AttributeError: 'FourCal' object has no attribute 'first'* 오류 발생.

setdata 메서드를 수행해야 객체 a의 객체변수 first와 second가 생성되기 떄문



이렇게 객체에 초깃값 설정해야할 필요가 있을떄는 setdata와 같은 메서드를 호출하여 초깃값을 설정하기보단는 생성자를 구현하는 것이 안전한 방법이다. **생성자(Constructor)란 객체가 생성될때 자동으로 호출되는 메서드를 의미한다** 파이썬 메서드 이름으로 _ ___init_ ___를 사용하면 이 메서드는 생성자가 된다. 다음과 같이 FourCal 클래스에 생성자를 추가해보자

```python
class FourCal:
    def __init__(self, first, second):
        self.first = first         # 매서드의 수행문
        self.second = second
> TypeError: __init__() missing 2 required positional arguments: 'first' and 'second'
```

생성자의 매개변수 first와 second에 해당하는 값이 전달되지 않았다. 위 오류를 해결하려면 다음처럼 first와 second에 해당되는 값을 전달하여 객체를 생성해야한다.



```python
class FourCal:
    def __init__(self, first, second):
        self.first = first         # 매서드의 수행문
        self.second = second
    def setdata(self,first,second): # 매서드의 매개변수
        self.first = first         # 매서드의 수행문
        self.second = second
    def add(self): # add메서드의 매개변수는 self이고 반환값을 result이다.
        result=self.first+self.second
        return  result # 해석 : result=4+2
    def sub(self):
        result=self.first-self.second
        return  result
    def mul(self):
        result=self.first*self.second
        return  result
    def div(self):
        result=self.first/self.second
        return  result

a=FourCal(4,2) 
# __init__메서드가 호출되면 setdata 메서드를 호출했을 때와 마찬가지로 first와 second라는
# 객체 변수가 생성될것이다.
print(a.first)
> 4
print(a.second)
> 2
```



##### 클래스의 상속

상속이란 '물려받다' 라는 뜻으로, '재산을 상속받다' 라고 할 때의 상속과 같은 의미이다. 어떤 클래스를 만들때 다른 클래스의 기능을 물러받을수 있게 만드는 것이다.



클래스를 상속하기 위해서는 다음처럼 클래스 이름 뒤 괄호 안에 상속할 클래스 이름을 넣어주면 된다

```
class 클래스 이름(상속할 클래스)
```

```python
class MoreFourCal(FourCal):
	 pass
```

MoreFourCal클래스는 FourCal 클래스를 상속했으므로 FourCal 클래스의 모든 기능을 사용할 수 있어야 한다.

```python
class MoreFourCal(FourCal):
    pass

a=MoreFourCal(4,2)
print(a.add())
> 6
print(a.mul())
> 8
```

원래 목적인 a의 b제곱을 계산하는 MoreFourCal 클래스를 만들어보자

```python
class MoreFourCal(FourCal):
    def pow(self):
        result = self.first ** self.second
        return result

a=MoreFourCal(4,2)
print(a.pow())
> 16
```

MoreFourCal 클래스로 만든 a객체에 값 4와 2를 설정한 후 pow 메서드를 호출하면 4의 2제곱인 16을 돌려주는 것을 확인할 수 있다.

상속은 MoreFourCal 클래스 처럼 기존 클래스는 그대로 놔둔채 클래스의 기능을 확장시킬떄 주로 사용한다.



##### 메서드 오버라이딩

```python
a=FourCal(4,0)
a.div()
> ZeroDivisionError: division by zero
```

FourCal 클래스의 객체a에 4와 0 값을 설정하고 div 메서드를 호출하면 4를 0으로 나누려고 하기때문에  ZeroDivisionError 오류 발생 하지만 0으로 나눌때 오류가 아닌 0으로  돌려주도록 만들고 싶다면 어떻게 해야할까?

```python
class SafeFourCal(FourCal):
    def div(self):
        if self.second==0:
            return 0
        else :
            return  self.first/self.second
```

SafeFourCal 클래스는 FourCal 클래스에 있는 div 메서드를 동일한 이름ㅇ로 다시 작성하였다. 이렇게 부모 클래스에 있는 메서드를 동일한 이르므으로 다시 만드는 것을 *메서드 오버라이딩*이라고 한다.

```python
class SafeFourCal(FourCal):
    def div(self):
        if self.second==0:
            return 0
        else :
            return  self.first/self.second

a=SafeFourCal(4,0)
print(a.div())
> 0
```



##### 클래스 변수

객체 변수와 성격이 다른 클래스 변수에 대해 알아보자.

```python
class Family:
    lastname="김"

a=Family() # a객체
b=Family() # b객체
print(a.lastname)
> 김
print(b.lastname)
> 김
```

만약 Family 클래스의 lastname을 다음과 같이 '박'이라는 문자열로 바꾸면?

```python
class Family:
    lastname="김"

a=Family()
b=Family()

Family.lastname='박' # lastname을 '박'으로 바꿈
print(a.lastname)
> 박
print(b.lastname)
> 박
```

클래스 변수 값을 변경했더니 클래스로 만든 객체의 lastname 값도 모두 변경된다는 것을 확인 할 수 있다. *즉, 클래스변수는 클래스로 만든 모든 객체에 공유 된다는 특징이 있다.*



## 모듈

모듈이란 함수나 변수 또는 클래스를 모아 놓은 파일것이다. 모듈은 다른 파이썬 프로그램에서 불러와 사용할 수 있게끔 만든 파이썬 파일이라고도 할 수 있다.



##### 모듈 만들기

```python
mod1 = open("C:/doit/mod1.py","w")
mod1 = open("C:/doit/mod1.py", "a")

#mod1.py
def add(a,b):
    return a+b
def sub(a,b):
    return a-b
```

##### 모듈불러오기













