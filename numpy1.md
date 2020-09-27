# numpy

* 넘파이 ndarray 개요

넘파이 array()함수는 파이썬의 리스트와 같은 다양한 인자를 입력 받아서 ndarray로 변환하는 기능

shape 변수는 ndarray의 크기, 즉 행과 열의 수를 튜플 형태로 가지고 있으며 ndarray 배열의 차원까지 알수 있음

```python
import numpy as np
array1=np.array([1,2,3])                     
print('array1 type:', type(array1))          
print('array1 array 형태:', array1.shape)   
> array1 type: <class 'numpy.ndarray'	   
> array1 array 형태: (3,)
    
array2=np.array([[1,2,3],[2,3,4]])
print('array2 type:', type(array2))
print('array2 array 형태:', array2.shape)
> array2 type: <class 'numpy.ndarray'>
> array2 array 형태: (2, 3)  # 2차원 array로 2개의 로우와 3개의 컬럼으로 구성 6개의 데이터
    
array3 = np.array([[1,2,3]])
print('array3 type:', type(array3)) # 1개의 로우와 3개의 컬럼으로 구성된 2차원 데이터를 의미
print('array3 array 형태:', array3.shape)
> array3 type: <class 'numpy.ndarray'>
> array3 array 형태: (1, 3)
```



* 각 array의 차원 이해 (ndarray.ndim)

```python
print('array1:{:0}차원, array2:{:1}차원, array3:{:2}차원'.format(array1.ndim,array2.ndim,array3.ndim))
> array1:1차원, array2:2차원, array3: 2차원
```



* ndarray의 데이터 타입

```python
list1=[1,2,3]
print(type(list1))
> <class 'list'>

array1=np.array(list1)
print(type(array1))
> <class 'numpy.ndarray'>

print(array1,array1.dtype)
> [1 2 3] int32
```

- int형과 string형이 섞여있는 리스트를 ndarray로 변경하면?

```python
list2=[1,2,'test']
array2=np.array(list2)
print(array2,array2.dtype)
> [1 2 3] int32
```

- int와 float형이 섞여있는 리스트를 ndarry로 변경하면?

```python
list3=[1,2,3.0]
array3=np.array(list3)
print(array3,array3.dtype)
> ['1' '2' 'test'] <U11

print(array3,array3.dtype)
> [1. 2. 3.] float64
```

ndrray는 모두 같은 데이터타입이어야 하므로 서로 다른 데이터 타입이 섞여 있을 경우 데이터 타입이 더 큰 데이터 타입으로 변환되어 int형이 유니코드문자열값으로 변환되었고 list3의 값도 float64형으로 변환되었습니다.

```python
array_int = np.array([1,2,3])
array_float = array_int.astype('float64')
print(array_float,array_float.dtype)
> [1. 2. 3.] float64

array_int1=array_float.astype('int32')
print(array_int1,array_int1.dtype)
> [1 2 3] int32

array_float1=np.array([1.1,2.1,3.1])
array_int2=array_float1.astype('int32')
print(array_int2,array_int2.dtype)
> [1 2 3] int32
```



