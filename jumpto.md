

# do it ! 점프 투 파이썬 

## 02장 파이썬 프로그래밍 기초

### 문자열 자료형

##### 1) 문자열 인덱싱과 슬라이싱

```python
a = "Life is too short, You need Python"
print(a[3])
> 'e'
```

파이썬은 0부터 숫자를 센다



* 문자열 인덱싱 활용하기

```python
a = "Life is too short, You need Python"
print(a[-0])
>'L'
```

 0과 -0은 똑같은 값을 가지기 때문에 a[-0]은 a[0]과 똑같은 값을 가진다.



* 문자열 슬라이싱이란?

```python
a = "Life is too short, You need Python"
print(a[0:4])
>'Life'
```

a[시작번호 : 끝번호]를 지정할때 끝번호에 해당하는 것은 포함시키지않는다.



##### 2) 문자열 포메팅

* 문자열 포맷 코드

| 코드 | 설명                        |
| ---- | --------------------------- |
| %s   | 문자열(String)              |
| %c   | 문자 1개(Character)         |
| %d   | 정수(Integer)               |
| %f   | 부동 소수(Floating-point)   |
| %o   | 8진수                       |
| %x   | 16진수                      |
| %%   | Literal % (문자열 '%' 자체) |

```python
number = 10
day = "three"
print("I ate %d apples. so I was sick for %s days" % (number,day))
> I ate 10 apples. so I was sick for three days
```

* 포매팅 연산자 %d와 %를 같이 쓸때는 %%를 쓴다.

```python
print("Error is %d%%." %98)
> Error is 98%.
```

* 포맷 코드와 숫자 함께 사용하기

  1)  정렬과 공백

  ```python
  print("%10s" % "hi") # 오른쪽정렬 왼쪽공백
  print("%-10sjane" % 'hi') # 왼쪽정렬 오른쪽공백
  ```

  2) 소수점 표현하기

  ```python
  print("%0.4f" % 3.4134234) # 소수점 네 번째 자리까지 나타내고 싶은경우
  print("%10.4f"% 3.42134234) 
  # 소수점 네번째 자리까지 나타내고 전체길이가 10개인 문자열 공간에서 오른쪽으로 정렬하는 예
  ```

  3) format 함수를 사용한 포맷팅

  ```python
  number=10
  day="three"
  print("I eat {0} apples. so I was sick for {1} days".format(number,day))
  > I eat 10 apples. so I was sick for three days
  ```

  2개 이상의 값을 넣을 경우 문자열의 {0},{1}과 같은 인덱스 항목이 format함수의 입력값으로 순서에 맞게 바뀐다.

-인덱스와 이름으로 혼용해서 넣기

```python
print("I ate {0} apples. so I was sick for {day} days".format(3, day="five"))
> I ate 3 apples. so I was sick for five days
print("{0:<10}".format("hi")) # 왼쪽 정렬
> hi        
print("{0:>10}".format("hi")) # 오른쪽 정렬
>         hi
print("{0:^10}".format("hi")) # 가운데 정렬
>     hi    
print("{0:=^10}".format("hi"))
> ====hi====
print("{0:!<10}".format("hi"))
> hi!!!!!!!!
print("{{ and }} ".format())
> { and } 
```



## 리스트 자료형

##### 1) 리스트는 어떻게 만들고 사용할까?

리스트명 = [요소1,요소2,요소3, ...]



##### 2) 리스트의 인덱싱과 슬라이싱

* 리스트의 인덱싱

```python
a = [1,2,3]
print(a[0])
> 1
print(a[0]+a[2])
> 4
print(a[-1])  # a[-1]은 문자열에서와 마찬가지로 리스트 a의 마지막 요솟값을 말한다.
> 3

a=[1,2,3,['a','b','c']]
print(a[0])
> 1
print(a[-1])
> ['a','b','c']
print(a[3])
> ['a','b','c']
print(a[-1][0])
> 'a'
```

* 삼중 리스트에서 인덱싱하기

```python
a = [1,2,['a','b',['Life','is']]]
```

리스트 안에 ['a','b', ['Life','is']]  리스트가 포함되어 있고, 그 리스트 안에 다시 ['Life','is']가 포함되어있다. 삼중 구조의 리스트이다.

이경우 'Life' 문자열만 끄집어내려면?

```python
a[2][2][0]
> 'Life'
```



* 리스트의 슬라이싱

```python
a=[1,2,3,4,5]
print(a[0:2])
> [1,2]

a="12345"
print(a[0:2])
> '12'
```



Q.  A=[1,2,3,4,5] 리스트에서 슬라이싱 기법을 사용하여 리스트 [2,3]를 만들어보자.

```python
A = [1,2,3,4,5]
result = A[1:3]
print(result)
> [2:3]
```



##### 3) 리스트 연산하기

* 초보자가 실수하기 쉬운 리스트 연산 오류

```python
a=[1,2,3]
a[2]+"hi"

> Traceback (most recent call last):
  File "C:/Users/mgk04.DESKTOP-8Q51H2D/PycharmProjects/TEST01/please.py", line 221, in <module>
    a[2]+"hi"
TypeError: unsupported operand type(s) for +: 'int' and 'str'
# 정수와 문자열을 당연히 더할수 없기 때문에 오류가 생김
```

```python
print(str(a[2])+"hi")
> 3hi
```



##### 리스트 수정과 삭제

리스트는 값을 수정하거나 삭제할 수 있다.

* 리스트에서 값 수정 삭제하기

  ```python
  a=[1,2,3]
  a[2]=4
  print(a)
  > [1,2,4]
  
  a=[1,2,3]
  del a[2]
  print(a)
  > [1,2]
  ```

  슬라이싱 기법을 사용하여 리스트의 요소 여러 개를 한꺼번에 삭제할 수도 있다.

  ```python
  a=[1,2,3,4,5]
  del a[2:]
  print(a)
  > [1:2]
  ```



* 리스트 관련 함수

  1) 리스트에 요소 추가(append)

  ```python
  a=[1,2,3]
  a.append(4)
  print(a)
  > [1,2,3,4]
  ```

  2) 리스트 정렬(sort)

  ```python
  a=[1,2,6,4,5]
  a.sort()
  print(a)
  >[1,2,4,5,6]
  ```

  3) 리스트 뒤집기(reverse)

  리스트 요소들을 순서대로 정렬한 다음 다시 역순으로 정렬하는 것이 아니라 그저  현재의 리스트를 그대로 거꾸로 뒤집는다.

  ```python
  a=['a','c','b']
  a.reverse()
  print(a)
  > ['b', 'c', 'a']
  ```

  4) 위치 반환(index)

  리스트에 x값이 있으면 x의 위치 값을 돌려준다.

  ```python
  a=[1,2,3]
  print(a.index(3))
  > 2
  print(a.index(1))
  > 0
  print(a.index(0))
  > Traceback (most recent call last):
    File "C:/Users/mgk04.DESKTOP-8Q51H2D/PycharmProjects/TEST01/please.py", line 238, in <module>
      print(a.index(0))
  ValueError: 0 is not in list
  # 리스트에 0이 존재하지 않기때문에 오류
  ```

  5)  리스트에 요소 삽입(insert)

  ```python
  a = [1,2,3]
  a.insert(0,4) # a[0]위치에 4를 추가해라!
  print(a)
  > [4,1,2,3]
  ```

  6) 리스트 요소 끄집어내기(pop)

  ```python
  a= [1,2,3]
  print(a.pop())
  > 3
  print(a)
  > [1,2]
  ```

  pop의 (x)는 리스트 x번째 요소를 돌려주고 그 요소는 삭제한다.

  a.pop(1)dms a[1]의 값을 끄집어 낸다.

  

  7) 리스트에 포함된 요소 x의 개수 세기(count)

  ```python
  a=[1,2,3,1]
  print(a.count(1))
  > 2
  ```

  1이라는 값이 리스트 a에 2개 들어있으므로 2를 돌려준다.

   8) 리스트 확장

  ```python
  a = [1,2,3]
  a.extend([4,5])
  print(a)
  > [1, 2, 3, 4, 5]
  
  b=[6,7]
  a.extend(b)
  print(a)
  > [1, 2, 3, 4, 5, 6, 7]
  ```

  

 ## 튜플 자료형

튜플(tuple)은 몇 가지 점을 제외하곤 리스트와 거의 비슷하며 리스트와 다른 점은 다음과 같다.

- 리스트는 []으로 둘러싸지만 튜플은 ()으로 둘러싼다.
- 리스트는 그 값의 생성, 삭제, 수정이 가능하지만 튜플은 그 값을 바 꿀 수 없다

---

```python
t1=()
t2=(1,) # 튜플은 t2=(1,)처럼 단지 1개의 요소만을 가질 때는 요소 뒤에 콤마(,) 반드시 붙여야함 
t3=(1,2,3)
t4=1,2,3 # 튜플은 t4처럼 괄호()를 생략해도 무방하다
t5=('a','b',('ab','cd'))
```

##### 튜플의 요소값을 지우거나 변경하려고 하면?

튜플 요솟값을 삭제하려 하면 불가능

```python
t1=(1,2,'a','b')
print(del t1[0])

> C:\Users\mgk04.DESKTOP-8Q51H2D\Anaconda3\python.exe C:/Users/mgk04.DESKTOP-8Q51H2D/PycharmProjects/TEST01/please.py
  File "C:/Users/mgk04.DESKTOP-8Q51H2D/PycharmProjects/TEST01/please.py", line 266
    print(del t1[0])
            ^
SyntaxError: invalid syntax
```

튜플 요솟값을 변경하려 하면 불가능

```python
t1=(1,2,'a','b')
print(t1[0]='c')

> C:\Users\mgk04.DESKTOP-8Q51H2D\Anaconda3\python.exe C:/Users/mgk04.DESKTOP-8Q51H2D/PycharmProjects/TEST01/please.py
  File "C:/Users/mgk04.DESKTOP-8Q51H2D/PycharmProjects/TEST01/please.py", line 269
    print(t1[0]='c')
         ^
SyntaxError: keyword can't be an expression
```



###### 튜플 다루기

- 튜플은 값을 변화시킬 수 없다는 점만 제외하면 리스트와 완전히 동일하다.

1. 인덱싱하기

   ````python
   t1 = (1,2,'a','b')
   print(t1[0])
   > 1 
   print(t1[1])
   > 2
   ````

2.  슬라이싱하기

   ```python
   t1=(1,2,'a','b')
   print(t1[1:])
   > (2, 'a', 'b')
   ```

   t1[1] 부터 튜플의 마지막 요소까지 슬라이싱하는 예이다.

3.  튜플 더하기

   ```python
   t1=(1,2,'a','b')
   t2=(3,4)
   print(t1+t2)
   > (1, 2, 'a', 'b', 3, 4)
   ```

4.  튜플 곱하기

   ````python
   print(t2*3)
   > (3, 4, 3, 4, 3, 4)
   ````

5.  튜플 길이 구하기

   ```python
   t1=(1,2,'a','b')
   print(len(t1))
   > 4
   ```

Q. (1,2,3) 이라는 튜플에 값 4를 추가하여 (1,2,3,4)를 만들어 출력해보자.

      ```python
a=(1,2,3)
print(a+(4,))
> (1,2,3,4)

      ```
     
      ```



## 딕셔너리 자료형

{Key1: Value1. Key2: Value2, Key3: Value3, ...}

```
dic = {'name':'pey','phone':'0119993323','birth':'1118'}
```

##### 딕셔너리 쌍 추가, 삭제하기

1) 딕셔너리 쌍 추가하기

```python
a={1:'a'}
a[2]='b'
print(a)
> {1: 'a', 2: 'b'}

a['name']='pey'
print(a) 
> {1: 'a', 2: 'b', 'name': 'pey'} #딕셔너리 a에 'name':'pey'라는 쌍이 추가되었다.

a[3]=[1,2,3]
print(a)
> {1: 'a', 2: 'b', 'name': 'pey', 3: [1, 2, 3]} 
 #딕셔너리 a에 key는 3, Value는 [1,2,3]을 가지는 한쌍이 또 추가되었다.
```

2) 딕셔너리 요소 삭제하기

```python
del a[1]  # key가 1인 key:value 쌍 삭제
print(a)
> {2: 'b', 'name': 'pey', 3: [1, 2, 3]}
```



##### 딕셔너리 사용하는 방법

1) 딕셔너리에서 Key  사용해 Value 얻기

```python
grade = {'pey': 10, 'juliet': 99}
print(grade['pey'])
> 10
print(grade['juliet'])
> 99
```

리스트나 튜플, 문자열은 요솟값을 얻고자 할 때 인덱싱이나 슬라이싱 기법 중 하나를 사용했다.

BUT, 딕셔너리는 단 한가지 방법 뿐

바로 Key를 사용해서 Value를 구하는 방법!!

```python
a={1:'a',2:'b'}
print(a[1])
> a
print(a[2])
> b
```

여기서 a[1] 의미 하는것은 리스트나 튜플의 a[1]과는 전혀 다르다.

딕셔너리 변수에서 [] 안의 숫자 1은 두번째 요소를 뜻하는 것이 아니라 Key에 해당하는 1을 나타낸다.

따라서,  a[1]은 딕셔너리 [1:'a',2:'b']에서 Key가 1인 것의 Value인 'a'를 돌려주게 된다.



2)  딕셔너리 만들 때 주의 할 상황

* 먼저 딕셔너리에서 Key 는 고유한 값이므로 중복되는 Key 값을 설정해 놓으면 하나를 제회한 나머지 것들이 모두 무시된다는 점을 주의해야한다. 다음 예에서 볼 수 있듯이 동일한 Key가 2개 존재할 경우 1: 'a' 쌍이 무시된다. 

```python
a={1:'a',1:'b'} # 1이라는 Key 값이 중복으로 사용
   print(a)
> {1: 'b'} # 1:'a'쌍이 무시됨
```

이렇게 중복되었을 때 1개를 제외한 나머지 Key: Value 값이 모두 무시되는 이유는 Key를 통해서 Value를 얻는 딕셔너리의 특징에서 비롯된다. 즉 동일한 Key가 존재하면 어떤 Key에 해당하는 Value를 불러야 할지 알 수 없기 때문이다. 

또 한가지 주의해야할 사항은 Key에 리스트는 쓸 수 없다!! 하지만 튜플은 Key로 쓸 수 있다. 딕셔너리의 Key로 쓸수 있느냐 없느냐는 Key가 변하는 값인지 변하지 않는 값인지에 달려있다. 



##### 딕셔너리 관련 함수

1) Key 리스트 만들기(keys)

```python
a= {'name':'pey','phone':'0119993323','birth':'1118'}
print(a.keys())
> dict_keys(['name', 'phone', 'birth'])
```

a.keys()는 딕셔너리 a의 Key만을 모아서 dict_keys 객체를 돌려준다.



2) dict_keys 객체를 리스트로 변환하려면 다음과 같이 하면 된다.

```python
a= {'name':'pey','phone':'0119993323','birth':'1118'}
print(list(a.keys()))
> ['name', 'phone', 'birth']
```

3) Value리스트 만들기(values)

```python
print(a.values())
> dict_values(['pey', '0119993323', '1118'])
```

4) Key,Value 쌍 얻기(items)

```python
print(a.items())
> dict_items([('name', 'pey'), ('phone', '0119993323'), ('birth', '1118')])
```

items 함수는 Key와 Value의 쌍을 튜플로 묶은 값을 dict_items 객체로 돌려준다.



5) Key:Value 쌍 모두 지우기(clear)

```python
print(a.clear())
> None
```

6)  Key로  Value 얻기 (get)

```python
a= {'name':'pey','phone':'0119993323','birth':'1118'}
print(a.get('name'))
> pey
print(a.get('phone'))
> 0119993323
```

get(x) 함수는 x라는 key에 대응되는 Value를 돌려준다. 앞에서 살펴보았듯이 a.get('name')은 a['name']을 사용햇을 때 와 동일한 결과 값을 돌려받는다.

* a['nokey'] 처럼 존재하지 않는 키로 값을 가져오라 할경우 a['nokey']는 Key 오류를 발생시키고 a.get('nokey')는 None을 돌려준다는 차이가 있다.



딕셔너리 안에 찾으려는 Key 값이 없을 경우 미리 정해 둔 디폴트 값을 대신 가져오게 하고 싶을 때에는 get(x,'디폴트값')을 사용하면 편리하다.

```python
print(a.get('foo','bar'))
> 'bar'
```



7)  해당 Key가 딕셔너리 안에 있는지 조사하기(in)

```python
a= {'name':'pey','phone':'0119993323','birth':'1118'}
print('name' in a)
> True
print('email' in a)
> False
```



## 집합자료형

##### 집합 자료형 특징

```python
s1 =set([1,2,3])
print(s1)
> {1, 2, 3}

s2=set("hello")
print(s2)
> {'l', 'o', 'e', 'h'}
```

- 중복을 허용하지 않는다.
- 순서가 없다.
  - 리스트나 튜플은 순서가 있기 떄문에 인덱싱을 통해 자료형의 값을 얻을 수 있지만 set자료형은 순서가 없기 때문에 인덱싱으로 값을 얻을 수 없다.
  - set 자료형에 저장된 값을 인덱싱으로 접근하려면 다음과 같이 리스트나 튜플로 변환 후 해야한다.

```python
s1= set([1,2,3])
l1=list(s1)
print(l1)
> [1, 2, 3]
print(l1[0])
> 1
```

##### 교집합,합집합,차집합 구하기

````python
s1=set([1,2,3,4,5,6])
s2=set([4,5,6,7,8,9])
````

* 교집합

  ```python
  print(s1&s2)
  > {4, 5, 6}
  print(s1.intersection(s2))
  > {4, 5, 6}
  ```

* 합집합

  ```python
  print(s1|s2)
  > {1, 2, 3, 4, 5, 6, 7, 8, 9}
  print(s1.union(s2))
  > {1, 2, 3, 4, 5, 6, 7, 8, 9}
  ```

* 차집합

  ```python
  print(s1-s2)
  > {1, 2, 3}
  print(s2-s1)
  > {8, 9, 7}
  print(s1.difference(s2))
  > {1, 2, 3}
  print(s2.difference(s1))
  > {8, 9, 7}
  ```

  

##### 집합 자료형 관련 함수

1) 값 1개 추가하기(add)

```python
s1 = set([1,2,3])
s1.add(4)
print(s1)
> {1, 2, 3, 4}
```

2) 값 열개 추가하기(update)

```python
s1 = set([1,2,3])
s1.update([4,5,6])
print(s1)
> {1, 2, 3, 4, 5, 6}
```

3) 특정 값 제거하기(remove)

```python
s1 = set([1,2,3])
s1.remove(2)
print(s1)
> {1, 3}
```



## 불자료형

불자료형이란 참(True)과 거짓(False)을 나타내는 자료형이다. 

```python
a = True
b = False
print(type(a)) 
> <class 'bool'>
```

```python
a = [1,2,3,4]
while a: # a가 참인 동안
    print(a.pop()) # 리스트의 마지막 요소를 하나씩 꺼낸다
> 4
> 3 
> 2
> 1
```

```python
while 조건문:
	수행할 문장
```

```python
if []: #[]는 비어있는 리스트 이므로 거짓이다.
    print("참")
else :
    print("거짓")
> 거짓
```

```python
if [1,2,3]: # [1,2,3]은 요솟값이 있는 리스트이기 때문에 참이다
    print("참")
else:
    print("거짓")
```



##### 불연산

```python
print(bool("Python"))
> True
```

'Python' 문자열은 빈 문자열이 아니므로 bool 연산의 결과로 불 자료형인 True를 돌려준다.

```python
print(bool([1,2,3]))
> True
print(bool([]))
> False
print(bool(0)) # 자료형중 숫자형은 0이 아닌 숫자는 참이고 
> False        #                0인 숫자는 거짓을 나타냄 그래서 False이다               
print(bool(3))
> True
```



##### 변수란?

```python
a=[1,2,3]
print(id(a))
> 2359808147848
```

id 함수는 변수가 가리키고 있는 객체의 주소 값을 돌려주는 파이썬 내장 함수이다.

##### 리스트를 복사할 때

```python
a=[1,2,3]
b=a
print(b)
> [1,2,3]
```

1) [:] 사용

* 리스트 전체를 가리키는 [:]을 사용하여 복사하는 것이다.

  ```python
  a=[1,2,3]
  b=a[:]
  a[1]=4
  print(a)
  > [1, 4, 3]
  print(b)
  > [1, 2, 3]
  ```

2) copy 모듈 사용

* from copy import copy

  ```python
  from copy import  copy
  a = [1,2,3]
  b = copy(a) # b=a[:]랑 같다
  print(b)
  > [1, 2, 3]
  ```

##### 변수를 만드는 여러 가지 방법

```python
a,b = ('python','life')
print(a,b)
> python life

(a,b)='python','life'
print(a,b)
> python life

[a,b]=['python','life']
print(a,b)
> python life

a=b='python'
print(a,b)
> python python
```

파이썬에는 두 변수의 값을 아주 간단히 바꿀 수 있다.

```python
a=3
b=5
a,b=b,a
print(a)
> 5
print(b)
> 3
```



### 연습문제

1. 홍길동 씨의 과목별 점수는 다음과 같다. 홍길도 씨의 평균 점수를 구해보자.

   | 과목 | 점수 |
   | ---- | ---- |
   | 국어 | 80   |
   | 영어 | 75   |
   | 수학 | 55   |

   ```python
   홍길동={'국어':80,'영어':75,'수학':55}
   print(sum(홍길동.values())/3)
   > 70.0
   ```

2.  자연수 13이 홀수인지 짝수인지 판변할 수 있는 방법에 대해 말해보자.

   ```python
   a=13
   if(a%2==0):
       print(True)
   else :
       print(False)
   > False
   ```

3.  홍길동 씨의 주민등록번호는 881120-1068234이다. 홍길동 씨의 주민등록번호를 연원일(YYYYMMDD) 부분과 그 뒤의 숫자 부분으로 나누어 출력해보자.

   ```python
   홍길동 = "881120-1068234"
   print("YYYMMDD :", 홍길동[:6])
   > YYYMMDD : 881120
   print("num :", 홍길동[7:])
   > num : 1068234
   ```

4.  주민등록번호 뒷자리의 맨 첫 번째 숫자는 성별을 나타낸다. 주민등록번호에서 성별을 나타내는 숫자를 출력해보자.

   ```python
   pin = "881120-1068234"
   print(pin[7])
   > 1
   ```

   

5.  다음과 같은 문자열 a : b : c : d가 있다. 문자열의 replace 함수를 이용하여 a#b#c#d로 바꿔서 출력해보자.

   ```python
   a="a:b:c:d"
   print(a.replace(':','#'))
   > a#b#c#d
   ```

6.  [1,3,5,4,2] 리스트를 [5,4,3,2,1]로 만들어 보자.

   ```python
   a = [1,3,5,4,2]
   a.sort()
   print(a)
   > [1, 2, 3, 4, 5]
   
   a.reverse()
   print(a)
   > [5, 4, 3, 2, 1]
   ```

7. ['Life','is','too','short'] 리스트를 Life is too short 문자열로 만들어 출력해 보자.

   ```python
   a = ['Life','is','too','short']
   result =' '.join(a)
   print(result)
   > Life is too short
   ```

8. (1,2,3) 튜플 값에 값 4를 추가하여 (1,2,3,4)를 만들어 출력해보자

9. 딕셔너리 a에서 'B'에 해당되는 값을 추출해 보자.

   ```python
   a={'A':90,'B':80,'C':70}
   result = a.pop('B')
   print(a)
   > {'A': 90, 'C': 70}
   print(result)
   > 80
   ```

10.  a. 리스트에서 중복 숫자를 제거해 보자.

    ```python
    a=[1,1,1,2,2,3,3,3,3,4,4,5]
    aSet=set(a)
    b=list(aSet)
    print(b)
    > [1, 2, 3, 4, 5]
    ```



# 프로그램의 구조를  쌓는다! 제어문

## if 문

#### 조건문이란 무엇인가?

if 조건문에서 '조건문'이란 참과 거짓을 판단하는 문장이다

* 돈이 3000원 이상 있거나 카드가 있다면 택시를 타고 그렇지 않으면 걸어 가라.

```python
money = 3000
card = True
if money>3000 or card :
    print("택시를 타라")
else :
    print("걸어가라")
> 택시를 타라 
```



x in s, x not in s

| in          | not in          |
| ----------- | --------------- |
| x in 리스트 | x not in 리스트 |
| x in 튜플   | x not in 튜플   |
| x in 문자열 | x not in 문자열 |

```python
print(1 in [1,2,3])
> True
print(1 not in [1,2,3])
> False
```

```python
print('a' in ('a','b','c'))
> True
print('j' not in 'python')
> True
```

  Q. 만약 주머니에 돈이 있으면 택시를 타고 없으면 걸어가라

```python
pocket = ['paper','cellphone','money']

if 'money' in pocket:
    print("택시타라")
else : print("걸어가라")
> 택시타라
```

Q. 주머니에 돈이 있으면 가만히 있고 주머니에 돈이 없으면 카드를 꺼내라.

```python
pocket = ['paper','cellphone','money']

if 'money' in pocket :
    pass
else:
    print("카드를 꺼내라")
```

pocket 리스트 안에 money 문자열이 있기 때문에 if문 다음 문장인 pass가 수행되고 아무 결과값도 보이지 않는다.



##### 다양한 조건을 판단하는 elif

```python
pocket=['paper','cellphone']
card = True
if 'money' in pocket: # 주머니에 돈이 있으면
    print("택시타고가라")
elif card :           # 주머니에 돈이 없고 카드가 있으면
    print("택시타고가라")
else :				  # 주머니에 돈도 없고 카드도 없으면 
    print("걸어가라")
```





### while문

반복해서 수행해야 할 경우 while문을 사용한다.

```python
treeHit = 0
while treeHit < 10:
    treeHit = treeHit +1
    print("나무를 %d번 찍었습니다." %treeHit)
    if treeHit == 10:
        print("나무 넘어갑니다.")
```

```python
coffee = 10
money = 300
while money:
    print("돈을 받았으니 커피를 줍니다")
    coffee=coffee-1
    print("남은 커피의 양은 %d개 입니다" %coffee)
    if coffee==0:
        print("커피가 다 떨어졌습니다. 판매를 중지합니다")
        break
```

###### while 문의 맨 처음으로 돌아가기

```python
a=0
while a < 10:
    a= a+1
    if a % 2 == 0 : continue
    print(a)
> 1
> 3
> 5 
> 7 
> 9
```

##### 무한 루프

```python
while True :
    print("Ctrl+c를 눌러야 while 문을 빠져나갈 수 있습니다.")
```



## for 문

파이썬의 직관적인 특징을 가장 잘 대변해 주는 것이 바로 for문이다.

---

#####  for문의 기본구조 

#####     for 변수 in 리스트(또는 튜플, 문자열)

​		수행할 문장1

​		수행할 문장 2

 1)  전형 적인 for문

```python
test_list = ['one','two','three']
for i in test_list:
    print(i)
> one
> two
> three
```

2) 다양한 for문의 사용

```python
a = [(1,2),(3,4),(5,6)]
for (first,last) in a:
    print(first + last)
> 3
> 7
> 11
```

3) for 문의 응용

 	Q. 총 5 명의 학생이 시험을 보았는데 시험 점수가 60점 넘으면 합격이고 그렇지 않으면 불합격이다. 			합격인지 불합격인지 결과를 보여주시오.

```python
marks = [90,25,67,45,80]
number = 0
for mark in marks:
    number = number + 1
    if mark >= 60:
        print("%d번 학생은 합격입니다" %number)
    else :
        print("%d번 학생은 불합격입니다" %number)
        
> 1번 학생은 합격입니다.
> 2번 학생은 불합격입니다.
> 3번 학생은 합격입니다.
> 4번 학생은 불합격입니다.
> 5번 학생은 합격입니다.
```
##### for문과 continue문

```python
marks=[90,25,67,45,80]
number=0
for mark in marks:
    number=number+1
    if mark < 60 : continue
    print("%d번 학생 축하합니다. 합격입니다." %number )
    
> 1번 학생 축하합니다. 합격입니다.
> 3번 학생 축하합니다. 합격입니다.
> 5번 학생 축하합니다. 합격입니다.
```

점수가 60점 이하인 학생일 경우 mark<60이 참이되어 continue문이 수행된다. 따라서 축하 메세지를 출력하는 부분인 print문을 수행하지않고 for문의 처음으로 돌아가게된다.

##### for문과 함께 자주 사용하는 range 함수

```python
a = range(0,10)
print(a)
```

range(0,10)은 0,1,2,3,4,5,6,7,8,9를 의미한다 

시작숫자와 끝 숫자를 지정하려면 range(시작숫자,끝숫자) 형태를 사용하는데 이때 끝숫자 형태는 포함되지않기 떄문이다.

```python
add=0
for i in range(1,11):
    add=add+i
print(add)
> 55
```

##### 리스트 내포 사용하기

```python
a=[1,2,3,4]
result=[]

for num in a:
    result.append((num*3))
print(result)
> [3, 6, 9, 12]
```

```python
a=[1,2,3,4]
result=[num*3 for num in a]
print(result)
> [3,6,9,12]
```

* ```python
  [표현식 for 항목 in 반복 가능 객체 if 조건]
  ```



## 연습문제

Q1. 다음 코드 결과값은 무엇일까?

```python
a = "Life is too short, you need python"
if "wife" is a:
    print("wife")
elif "python" in a and "you" not in a:
    print("python")
elif "short" not in a:
    print("shirt")
elif "need" in a:
    print("need")
else :
    print("none")
> need
```



Q2. while문을 사용해 1부터 1000까지의 자연수 중 3의 배수의 합을 구해보자.

```python
result =0
i = 1
while i<=1000:
    if i%3==0 :
        result = result+i
    i = i + 1
print(result)
> 166833
```



Q3. while문을 사용하여 다음과 같이 별(*)을 표시하는 프로그램을 작성해보자

```python
i=0
while True:
    i+=1
    if i>5: break
    print('*'*i)
    
> *
> **
> ***
> ****
> *****
```



Q4. for문을 사용해 1부터 100까지 숫자를 출력해보자.

```python
for i in range(1,101):
    print(i)
```



Q5. A학급에 총 10명의 학생이 있다. 이 학생들의 중간고사 점수는 다음곽 ㅌ다.

[70,60,55,75,95,90,80,80,85,100]

for문을 사용하여 A학급의 평균 점수를 구해보자.

```python
A = [70,60,55,75,95,90,80,80,85,100]
total = 0
for score in A:
    total += score
average = total / len(A)
print(average)
```



Q6. 리스트 중에 홀수에만 2를 곱하여 저장하는 다음 코드가 있다.

```python
numbers=[1,2,3,4,5]
result=[]
for n in numbers :
    if n % 2==1 :
        result.append(n*2)
print(result)

> [2, 6, 10]
```

```python
result = [n*2 for n in numbers if n%2==1]
print(result)

> [2, 6, 10]
```

```
# 리스트 내포의 일반 문법 잘이해하기
[표현식 for 항목 in 반복 가능 객체 if 조건]
```



## 04 장 함수

##### 파이썬 함수의 구조

```
def 함수 이름(매개변수):
	수행할 문장1
	수행할 문장2
```

```python
def add(a,b):
    return a+b
print(add(3,4))
> 7
```

##### 입력값과 결과값에 따른 함수의 형태

1) 일반적인 함수

* 입력값이 있고 결과값이 있는 함수가 일반적인 함수

```
def 함수 이름(매개변수):
	수행할 문장
	...
	return 결과값
```

* 입력값이 없는 함수

```python
def say():
	return 'Hi'
a= say()
print(a)
> Hi
```

* 결과값이 없는 함수

```python
def add(a,b):
	print("%d,%d의 합은 %d입니다."%(a,b,a+b))

print(add(3,4))
> 3,4의 합은 7입니다.
```

결과값이 없는 함수는 호출해도 돌려주는 값이 없기 떄문에 다음과 같이 사용한다 즉 결과값이 없는 함수는 다음과 같이 사용한다

```
함수이름(입력인수,입력인수2,...)
```

결과 값이 진짜 없는지 확인을 해보자

```python
a=add(3,4)
print(a)
> 3,4의 합은 7입니다.
> None
```

* '3,4의 합은 7입니다' 라는 문장을 출력해 주었는데 왜 결과값이 없다는 것일까? print문은 함수의 구성 요소 중 하나인 <수행할 문장>에 해당하는 부분일 뿐이다. 결과값은 당연히 없다. 결과값은 오직 return 명령어로 돌려받을 수 있다.
* a는 None이다 None이란 거짓을 나타내는 자료형이라고 생각하면 된다.



##### 입력 값도 결과값도 없는 함수

```python
def say():
	print('Hi')

say()
> Hi
```

입력 인수를 받는 매개변수도 없고 return문도 없으니 입력값도 결과값도 없는 함수이다. 즉 입력값도 결과값도 없는 함수는 다음과 같이 사용한다

```
함수이름()
```

##### 매개변수 지정하여 호출하기

```python
def add(a,b):
	return a+b

result = add(a=3,b=7)
print(result)
> 10 
```

매개변수를 지정하면 다음과 같이 순서에 상관없이 사용할 수 있다는 장점이있다. 

```python
result = add(a=5,b=3)
print(result)
> 8
```

##### 입력값이 몇개가 될지 모를 떄는 어떻게 해야할까?

```
def 함수이름(*매개변수)
	수행할 문장
	...
```

 ##### 여러개의 입력값을 받는 함수 만들기

```python
def add_many(*args):
	result = 0
	for i in args:
		result = result + i
	return result

result=add_many(1,2,3)
print(result)
> 6

result=add_many(1,2,3,4,5,6,7,8,9,10)
print(result)
> 55
```

```python
def add_mul(choice,*args):
	if choice=="add":
		result=0
		for i in args:
			result= result+i
	elif choice=="mul":
		result=1
		for i in args:
			result=result*i
	return  result

result = add_mul('add',1,2,3,4,5)
print(result)
> 15

result = add_mul('mul',1,2,3,4,5)
print(result)
> 120
```



#### 키워드 피라미터

```python
def print_kwargs(**kwargs):
	print(kwargs)

print_kwargs(a=1)
> {'a': 1}
print_kwargs(a=1,b=3)
> {'a': 1, 'b': 3}
```

모두 딕셔너리로 만들어져 출력된다는 것을 알수 있다. 즉 **를 붙이면 매개변수 kwarge는 딕셔너리가 되고 모든 key=value 형태의 결과값이 그 딕셔너리에 저장된다.



##### 함수의 결과값은 언제나 하나이다.

```python
def add_and_mul(a,b):
	print(a+b,a*b)

result=add_and_mul(3,4)
result 
> 7 12 #튜플 값을 의미
```

함수의 결과값은 a+b 와 a*b는 튜플 값 하나인(a+b, a * b)로 돌려준다.



```python
def add_and_mul(a,b):
	return a+b
	return a*b

result = add_and_mul(2,3)
print(result)
> 5 
```

위와 같이 return문은 2번 사용하면 2개의 결과값을 돌려주지 않을까? 

함수는 return문을 만나는 순간 결과값을 돌려준 다음 함수를 빠져나가게 된다.



##### return의 또 다른 쓰임새

특별한 상황일 때 함수를 빠져나가고 싶다면 return을 단독으로 써서 함수를 즉시 빠져나갈 수있다.

```python
def say_nick(nick):
	if nick=="바보":
		return
	print("나의 별명은 %s 입니다." %nick)

print(say_nick('야호'))
> 나으 별명은 야호 입니다.
print(say_nick('바보'))
```

위 함수는 '별명'을 입력으로 전달받아 출력하는 함수이다. 이 함수 역시 변환 값은 없다. 만약에 입력값으로 '바보'라는 값이 들어오면 문자열을 출력하지 않고 함수를 즉시 빠져나간다.



##### 매개변수에 초깃갓 미리 설정하기

매개변수에 초깃값을 미리 설정해 주는 경우이다.

```python
def say_myself(name,old,man=True) : 
	print("나의 이름은 %s입니다." %name)    
	print("나이는 %d살입니다." %old)       
	if man:                         
		print("남자입니다.")             
	else:                           
		print("여자입니다.")             
                                    
say_myself("박응용",27) 
> 나의 이름은 박응용입니다.
> 나이는 27살입니다.
> 남자입니다.

say_myself("박응용",27,True)    
> 나의 이름은 박응용입니다.
> 나이는 27살입니다.
> 남자입니다.
```

함수의 매개변수에 들어갈 값이 항상 변하는 것이 아닐 경우에는 이렇게 함수의 초기값을 미리 설정해 두면 유용하다. 위 예에서 함수를 사용한 2가지 방법은 모두 동일한 결과를 출력한다.

만약 man의 초기값을 False로 잡아준다면?

```python
def say_myself(name,old,man=False) :   
	print("나의 이름은 %s입니다." %name)       
	print("나이는 %d살입니다." %old)          
	if man:                            
		print("남자입니다.")                
	else:                              
		print("여자입니다.")          
say_myself("박응용",27) 
> 나의 이름은 박응용입니다.
> 나이는 27살입니다.
> 여자입니다.      
```

**함수의 초기값을 설정할 때 주의할 것이 하나있다**

**초기값을 설정한 매개변수의 위치이다**

```python
def say_myself(name,man=False, old) : 
	print("나의 이름은 %s입니다." %name)      
	print("나이는 %d살입니다." %old)         
	if man:                           
		print("남자입니다.")               
	else:                             
		print("여자입니다.")  
> say_myself("박응용",27) 
```

```
SyntaxError: non-default argument follows default argument
```

위 오류 메시지는 초기값을 설정해 놓은 매개변수 뒤에 초기값을 설정해 놓지 않음 매개변수는 사용할 수 없다는 뜻이다. 즉 매개변수로(name,old,man=False)은 되지만 (name,man=False, old)는 안된다는 것이다. 

** 초기화시키고 싶은 매개변수를 항상 뒤쪽에 놓는 것을 잊지 말자  **



##### 함수 안에서 선언한 변수의 효력 범위

```python
a=1              # 함수 밖의 변수 a    
def vartest(a):  # vartest 함수 선언 
	a=a+1         
                  
vartest(a)     # vartest 함수의 입력값으로 a를 줌   
print(a)       # a를 출력   
```

당연히 vartest 함수에서 매개변수 a의 값에 1을 더했으니까 2가 출력 될것 같지만 프로그램 소스를 작성해서 실행해 보면 결과값은 1이 나온다. 그 이유는 함수 안에서 새로 만든 매개변수는 함수 안에서만 '함수만의 변수'이기 때문이다. 즉, def vartest(a)을 입력값을 전달받는 매개변수 a는 함수 안에서만 사용하는 변수이지 함수 밖의 변수 a가 아니라는 뜻이다.



##### 함수 안에서 함수 밖의 변수를 변경하는 방법

vartest이라는 하무를사용해서 함수 밖의 변수 a를 1만큼 증가시킬 수 있는 방법은 없을까? 

1. return 사용하기 

   ```python
   a=1              
   def vartest(a):  
   	a=a+1        
   	return a     
   a = vartest(a)   #vartest(a)의 결과값을 함수 밖의 변수 a에 대입
   print(a)         
   > 2
   ```

2. global 명령어 사용하기

   ```python
   a=1
   def vartest():
   	global a
   	a = a + 1
   
   vartest()
   print(a)
   > 2
   ```

3. lambda

   lambda 함수를 생성할 때 사용하는 예약어로 def와 동일한 역할을 한다. 보통 함수를  한줄로 간결하게 만들 때 사용한다. 

   ```
   lambda 매개변수1, 매개변수2,... : 매개변수를 사용한 표현식
   ```

   ```python
   add = lambda a,b : a+b
   result =add(3,4)
   print(result)
   > 7
   ```



### 사용자 입력와 출력

##### 사용자 입력

input은 입력되는 모든 것을 문자열로 취급한다.

```
input("질문내용")
```



##### 큰따옴표("")로 둘러싸인 문자열은 + 연산과 동일하다

```python
print("life""is""too short")
> lifeistoo short
print("life"+"is"+"too short")
> lifeistoo short
```

##### 문자열 띄어쓰기는 콤마로 한다

```python
print("life","is","too short")
> life is too short
```

##### 한줄에 결과값 출력하기

```python
for i in range(10):
	print(i,end='')
> 0123456789
```



## 연습문제

1. 주어진 자연수가 홀수인지 짝수인지 판별해주는 함수 (is_odd)를 작성해보자

   ```
   def is_odd(number):
   	if number%2==1:
   		return True
   	else:
   		return False
   ```

2. 입력으로 들어오는 모든 수의 평균 값을 계산해 주는 함수를 작성해보자(단 입력으로 들어오는 수의 개수는 정해지지 않았다.)

   ```python
   def avg_numbers(*args):
   	result = 0
   	for i in args:
   		result += i
   	return result/len(args)
   
   print(avg_numbers(1,2))
   > 1.5
   print(avg_numbers(1,2,3,4,5))
   > 3.0
   ```













