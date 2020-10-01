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

