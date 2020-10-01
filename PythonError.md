# Python Error

파이썬으로 크롤링을 시도하던 중 403 Foribidden 에러가 남.

구글링을 해보니 원인은 requests로 접근하는걸 비정상적인 접근으로 본다.

```python
url="http://jolse.com/category/toners-mists/43/"
result=requests.get(url)
bs_obj=BeautifulSoup(result.content,"html.parser")
print(bs_obj)
```

 Forbidden 오류가 뜨는 것을 확인 이를 해결하기 위하여 ** 진행

```python
**headers = {'User-Agent': 'Mozilla/5.0'}
url="http://jolse.com/category/toners-mists/43/"
result=requests.get(url,headers=headers)**
bs_obj=BeautifulSoup(result.content,"html.parser")
print(bs_obj)
```

-------------------------------------------------------------------------------------------------------

### 파일 업로드 error

```python
file = open("C:\Users\mgk04.DESKTOP-8Q51H2D\Desktop\문재인대통령취임사.txt",'r')
lists = file.readlines()
file.close()
lists
```

```python
SyntaxError: (unicode error) 'unicodeescape' codec can't decode bytes in position 2-3: truncated \UXXXXXXXX escape
```

```python
file = open("C:/Users/mgk04.DESKTOP-8Q51H2D/Desktop/문재인대통령취임사.txt",'r')
lists = file.readlines()
file.close()
lists
```

```python
UnicodeDecodeError: 'cp949' codec can't decode byte 0xed in position 6: illegal multibyte sequence
```

```python
file = open("C:/Users/mgk04.DESKTOP-8Q51H2D/Desktop/문재인대통령취임사.txt",'r',encoding='utf-8')
lists = file.readlines()
file.close()
lists              #제대로된 결과값이 나옴
```



