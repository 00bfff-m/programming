# web2python_ind

쓰는 이유: HTML과 CSS만 사용하여 웹 application 만들다가 python을 사용하면 더 효율적이기 때문에

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
import codecs, sys, cgi, os 
```

```
sys.stdout = codecs.getwriter("utf-8")(sys.stdout.detach()) # stdout의 인코딩을 UTF-8로 강제 변환한다
print()
```
-> 웹 application을 수정하거나 만들 때 한글로 텍스트를 입력하게 해주는 역할  

## for loop를 사용하여 query string으로 된 글목록 생성  
**query string:** 사용자가 입력 데이터를 전달하는 방법중의 하나로, url 주소에 미리 협의된 데이터를 파라미터를 통해 넘기는 것을 말한다. ex) index.py?key1=value1&key2=value2... 


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

**`<a></a>`**: 하이퍼링크 삽입, ex) `<a href=링크 주소></a>`: 

```
#data directory에 있는 file list를 file이라는 변수로 지정
files = os.listdir('data') 

listStr = '' #for loop를 사용하려면 비어 있는 자료형이 필요함 

for item in files: #각 file마다 아래와 같은 format으로 된 변수(글목록) 생성
    listStr = listStr + '<li><a href="index.py?id={name}">{name}</a></li>'.format(name=item) 
```


## 조건문을 사용하여 query string에 반응 및, 글의 수정, 삭제 기능 추가

```
#index.py?id를 받는 역할
form = cgi.FieldStorage()
```
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
else: #만약 query string이 없으면 'welcome, Hello web' 출력 
    pageId = '안녕하세요'
    description = '뭐하지...'
    update_link = ''
    delete_action = ''
```

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
'''.format(title = pageId, desc = description, list = listStr, update = update_link, delete = delete_action)) #formating을 사용하여 title pageId라는 변수로 치환
```
