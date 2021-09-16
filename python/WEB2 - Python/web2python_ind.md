# web2python_ind

쓰는 이유: HTML과 CSS만 사용하여 웹 application 만들다가 python을 사용하면 더 효율적이기 때문에  
**query string:** 사용자가 입력 데이터를 전달하는 방법중의 하나로, url 주소에 미리 협의된 데이터를 파라미터를 통해 넘기는 것을 말한다. ex) index.py?key1=value1&key2=value2...  
**CGI(Common Gateway Interface):** 웹서버(e.g. apache)와 CGI application(e.g. 지금 사용하는 index.py) 사이에 서로 상호작용을 할 수 있게 해주는 표준화된 약속  
**API(Application Programming Interface):** 애플리케이션을 구현하기 위해서 시간 순서대로 배치해야 할 기능들 ex) print, listdir 등은 python에 내장되어 있는 API  
**application:** 기존의 기능을 응용하여 새로운 기능을 만드는 것(= program: 시간의 순서에 따라 일어나는 일들)  
파이썬의 부품은 함수들(function), 결합 방법은 문법(syntax)  

## preparation  
```
#!C:\Users\user\anaconda3\python.exe 
```
-> apache와 python를 연결하는 용도로 추측  

```
print("content-type:text/html; charset=UTF-8") 
```
-> 웹서버에게 text/html을 처리해달라고 명령  

```
#필요한 모듈 불러오기  
#view: 글목록을 생성해주는 모듈, view.md 참고
import codecs, sys, cgi, os, view, html_sanitizer
```

```
sys.stdout = codecs.getwriter("utf-8")(sys.stdout.detach()) # stdout의 인코딩을 UTF-8로 강제 변환한다
print()
```
-> 웹 application을 수정하거나 만들 때 한글로 텍스트를 입력하게 해주는 역할  

## for loop를 사용하여 query string으로 된 글목록 생성  

**`<li></li>`**: html 태그, 목록 생성<br> 
ex)  
~~~
<ol> <!--<ol></ol>: ordered list-->
  <li>항목 1</li> 
  <li>항목 2</li>
</ol>

<ul> <!--<ul></ul>: unordered list-->
  <li>항목 1</li>
  <li>항목 2</li>
</ul>
~~~

## 조건문을 사용하여 query string에 반응 및, 글의 수정, 삭제 기능 추가
**`<form></form>`:** 사용자가 입력한 데이터를 한번에 웹으로 전송  
ex) `<form action="form을 전송할 서버쪽 스크립트 파일" method="get(default) or post">` (get보다는 post방식이 보안에 적합)
**`<a></a>`**: 하이퍼링크 삽입, ex) `<a href=링크 주소></a>`: 

```
form = cgi.FieldStorage()
```
cgi.FieldStorage(): 이전에 들어온 id 데이터를 받는 역할 

```
if "id" in form: 
    pageId = form["id"].value #만약 query string이 있으면 query string과 그에 맞는 description 출력
    description = open('data/'+pageId, 'r',encoding='UTF-8').read()
    update_link = '<a href="update.py?id={}">update</a>'.format(pageId) #만약 query string이 있으면 update_link변수 생성
    delete_action = ''' #만약 query string이 있으면 delete_action 변수 생성
        <form action="process_delete.py" method="post">
            <input type="hidden" name="pageId" value="{}"> 
            <input type="submit" value="delete">
        </form>
    '''.format(pageId)
else: #만약 query string이 없으면 정해둔 string 출력, update와 delete 기능은 넣지 않기
    pageId = '안녕하세요'
    description = '뭐하지...'
    update_link = ''
    delete_action = ''
```
**`<!doctype hyml>`:** 웹 문서의 유형을 html로 지정  
```
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
'''.format(
    title = pageId,
    desc = description,
    list = view.getList(),
    update = update_link,
    delete = delete_action,
    check = form))
```
