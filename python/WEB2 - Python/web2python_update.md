```
#!C:\Users\user\anaconda3\python.exe
print("content-type:text/html; charset=UTF-8\n") #웹서버에게 text/html을 처리해달라고 명령

print()
import cgi, os, view
```

form = cgi.FieldStorage()
if "id" in form: #만약 query string이 없으면 'welcome, Hello web', 있으면 query string, 그에 맞는 description 출력
    pageId = form["id"].value
    description = open('data/'+pageId, 'r',encoding='UTF8').read()
else:
    pageId = 'Welcome'
    description = 'Hello, web'
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
  <form action="process_update.py" method="post"> <!--<form></form>: URL query string을 만들어 주는 역할-->
      <input type="hidden" name="pageId" value="{form_default_title}"> <!--title을 바꿔도 error가 생기지 않게끔 해주는 역할-->
      <p><input type="text" placeholder="title" name="title" value="{form_default_title}"></p>  <!--<p></p>: 줄바꿈-->
      <p><textarea rows="4" placeholder="description" name="description" value="{form_default_description}"></textarea></p> <!--<textarea rows="number"></textarea>: 여러 줄을 입력할 수 있는 UI 생성-->
      <p><input type="submit"></p>
  </form>
</body>
</html>
'''.format(
    title = pageId,
    desc = description,
    list = view.getList(),
    form_default_title = pageId,
    form_default_description = description)) #formating을 사용하여 title pageId라는 변수로 치환

