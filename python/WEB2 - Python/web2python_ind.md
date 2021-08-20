# web2python_ind

쓰는 이유: HTML과 CSS만 사용하여 웹 브라우저를 만들다가 python을 사용하면 브라우저의 용량을 줄일 수 있다나 뭐라나...

```
#!C:\Users\user\anaconda3\python.exe
print("content-type:text/html; charset=UTF-8") #웹서버에게 text/html을 처리해달라고 명령
import codecs, sys, cgi, os #모듈 불러오기
sys.stdout = codecs.getwriter("utf-8")(sys.stdout.detach()) # stdout의 인코딩을 UTF-8로 강제 변환한다
print()

files = os.listdir('data') #data directory에 있는 file list를 file이라는 변수로 지정

listStr = ''
for item in files: #각 file마다 아래와 같은 format으로 된 변수(글목록) 생성
    listStr = listStr + '<li><a href="index.py?id={name}">{name}</a></li>'.format(name=item) #query string: ?id 어쩌고 하는 거

form = cgi.FieldStorage() #index.py?id를 받는 역할
if "id" in form: #만약 query string이 없으면 'welcome, Hello web', 있으면 query string, 그에 맞는 description 출력
    pageId = form["id"].value
    description = open('data/'+pageId, 'r',encoding='UTF-8').read()
    update_link = '<a href="update.py?id={}">update</a>'.format(pageId) #만약 query string이 있으면 update_link변수 생성
    delete_action = '''
        <form action="process_delete.py" method="post">
            <input type="hidden" name="pageId" value="{}">
            <input type="submit" value="delete">
        </form>
    '''.format(pageId)
else:
    pageId = '안녕하세요'
    description = '뭐하지...'
    update_link = ''
    delete_action = ''
print(pageId)
print('''<!doctype html>
<html>
<head>
  <title>WEB1 - Welcome</title>
  <meta charset='UTF-8'/>
</head>
<body>
  <h1><a href="index.py">WEB</a></h1>
  <ol>{list}</ol>
  <a href="create.py">create</a>
  {update}
  {delete}
  <h2>{title}</h2>
  <p>{desc}</p>
</body>
</html>
'''.format(title = pageId, desc = description, list = listStr, update = update_link, delete = delete_action)) #formating을 사용하여 title pageId라는 변수로 치환
```
