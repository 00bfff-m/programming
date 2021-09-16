# 글 생성 기능 구현하기

```
#!C:\Users\user\anaconda3\python.exe
print("content-type:text/html; charset=UTF-8\n") #웹서버에게 text/html을 처리해달라고 명령
import codecs, sys, cgi, os, view #cgi, os, view라는 모듈 불러오기
sys.stdout = codecs.getwriter("utf-8")(sys.stdout.detach()) # stdout의 인코딩을 UTF-8로 강제 변환한다
print()
```

```
form = cgi.FieldStorage()
if "id" in form: #만약 query string이 없으면 'welcome, Hello web', 있으면 query string, 그에 맞는 description 출력
    pageId = form["id"].value
    description = open('data/'+pageId, 'r',encoding='UTF8').read()
else:
    pageId = 'Welcome'
    description = 'Hello, web'
```
```
print(pageId)
print('''<!doctype html>
<html>
<head>
  <title>WEB1 - Welcome</title>
  <meta charset="utf-8">
</head>
<body>
  <h1><a href="index.py">WEB</a></h1>
  <ol>{list}</ol>
  <a href="create.py">create</a></h1>
  <form action="process_create.py" method="post"> <!--<form></form>: URL query string을 만들어 주는 역할-->
      <p><input type="text" placeholder="title" name="title"></p>  <!--<p></p>: 줄바꿈-->
      <p><textarea rows="4" placeholder="description" name="description"></textarea></p> <!--<textarea rows="number"></textarea>: 여러 줄을 입력할 수 있는 UI 생성-->
      <p><input type="submit"></p>
  </form>
</body>
</html>
'''.format(
    title = pageId,
    desc = description,
    list = view.getList())) #formating을 사용하여 title pageId라는 변수로 치환
```
