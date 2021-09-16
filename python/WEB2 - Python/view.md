# 글목록을 구현하는 모듈 생성하기

```
#필요한 모듈 불러오기
import os, html_sanitizer
```
## 글목록을 생성해주는 함수 생성
```
def getList(): 
    sanitizer = html_sanitizer.Sanitizer()
    files = os.listdir('data') #data directory에 있는 file list를 file이라는 변수로 지정
    listStr = ''
    for item in files: 
        listStr = listStr + '<li><a href="index.py?id={name}">{name}</a></li>'.format(name=item)
    return listStr #최종적으로 각 file마다 위와 같은 format으로 된 변수(글목록)인 listStr값 반환
 ```
