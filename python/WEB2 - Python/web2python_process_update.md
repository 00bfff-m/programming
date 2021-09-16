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
opened_file.write(description) #description을 넣은 파일 생성
opened_file.close()
os.rename('data/'+pageId, 'data/'+title)

#redirection
print("Location: index.py?id="+title) #웹서버가 웹브라우저에게 index.py?id="+title이라는 주소로 보내달라고 명령
print()
```
