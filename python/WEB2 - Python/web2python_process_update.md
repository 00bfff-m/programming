# 글 수정 기능 구현(updata.md에서 제출한 form 처리 구현)

```
#!C:\Users\user\anaconda3\python.exe
import cgi, os
```
```
form = cgi.FieldStorage() #index.py?id를 받는 역할
pageId = form["pageId"].value
title = form["title"].value #update.py에서 받은 title value를 변수에 저장
description = form["description"].value #update.py에서 받은 description value를 변수에 저장
```
```
opened_file = open('data/'+pageId, 'w') #data라는 폴더 안에 title이라는 파일 열기
opened_file.write(description) #update.py에서 받은 description value를 이전에 열었던 파일에 작성
opened_file.close()
os.rename('data/'+pageId, 'data/'+title) #파일의 제목을 기존 pageId에서 수정하고자 하는 title value로 바꾸기 

#redirection
print("Location: index.py?id="+title) #웹서버가 웹브라우저에게 index.py?id="+title이라는 주소로 보내달라고 명령
print()
```
