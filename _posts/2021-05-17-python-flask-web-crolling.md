---
layout: post

title: 파이썬&플라스크- 플라스크로 웹사이트 만들기

tags: [python]

image:
---

### 플라스크?

- 파이썬으로 웹사이트를 만들 수 있게 해주는 "micro" 프레임워크이다.
- "micro"란 여러가지 설정을 사용자가 셋팅할 필요 없이 자동으로 해준다는 의미이다.
- 아주 편한 프레임워크!
- 플라스크를 사용하려면 따로 설치할 필요가 있는데, 나같은 경우 repl.it으로 실습을 해서 따로 설치하진 않았다.
- 아래 한줄을 입력하면 됐기에.. 설치는 vsc로 다뤄볼 때 찾아볼듯..

```python
from flask import Flask
```

### 플라스크 첫 셋팅

- 서버를 생성한다.

```python
from flask import Flask

app = Flask("appName")

app.run(host="호스트 주소") // repl.it 환경에선 0.0.0.0으로 입력
```

<img src="/images/posts/flask_01.png">
짠. 서버 생성 완료!
Not Found는 신경쓰지 말도록 하자. 지금은 웹에 띄울 데이터도 요소도 아무것도 없다는 것이다.

<br/>

- index.html을 홈으로 만들어 보자.
- / = root 를 의미. root는 뿌리라는 뜻인데, 여기선 출발점이라고 이해하면 좋을 듯 하다.
- www.google.com = www.google.com/ 과 같다는 뜻이다!
- url에 웹페이지를 연결하기 위해선 route() 함수를 사용하면 된다. 괄호 안에는 정의된 url root주소(/로 시작하는)를 입력하면 된다.

```python
# from flask import Flask

app = Flask("appName")

@app.route("/")
def functionName():
  return "hello!"

@app.route("/contact")
def potato():
  return "here are contact us!"

app.run(host="0.0.0.0")
```

<br/>
- 사용자가 /contact에 접속할 때 potato함수를 실행하고 싶은 걸 파이썬이 어떻게 아는 걸까?
- @ 로 인식한다.
- @은 데코레이터 인데, 바로 아래에 있는 함수를 찾는다. 그 함수를 decorate(꾸미다) 역할로 코드를 실행해준다.
- 그래서 파이썬은 "/contact 로 접속 요청이 들어오면 potato를 실행하면 되는군!" 하고 인식하는 것이다.
- @app.route() + 함수가 기본 구조이다.

### html 페이지 연결하기

- return "text"를 했을 때 html에서 "text"를 바로 뿌려주는 걸 보면
- 데코레이터가 인식하는 함수 안에 html 을 써도 되지만.. 그것은 너무나도 비효율적이다.
- 템플릿 폴더 안에 html 문서를 작성하면 플라스크에서 그 문서를 인식할 수 있다.
- 먼저 render_template를 임포트 해야 해당 함수를 사용할 수 있다.
- return 에 render_template("문서이름.html")

<img src="/images/posts/flask_04.png">

```python
from flask import Flask, render_template

# app = Flask("appName")

@app.route("/")
def home():
  return render_template("potato.html")

# app.run(host="0.0.0.0")
```

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>potato</title>
  </head>
  <body>
    <h1>Job Search</h1>
    <form>
      <input type="text" placeholder="What job do you want" />
      <button type="submit">Search</button>
    </form>
  </body>
</html>
```

<img src="/images/posts/flask_02.png">
실행하면 웹 상에서 html에 입력한 코드가 렌더링된다.
- flask는 이렇게 설정되어 있는 함수가 많아 최소한의 구성 요소와 요구 사항을 제공한다. 그래서 시작하기 쉽고 필요에 따라 유연하게 사용할 수 있다.

### html에서 입력한 데이터 받아오기

- html에서 데이터를 서버에 넘겨 줄 때 사용하는 태그는 form이다.
- form 안에 input 자식의 value(값)들을 모아서 서버에 전송해준다.
- form에는 기본적으로 2가지 프로퍼티가 있는데, action과 method이다.
- action은 어느 url로 데이터를 보낼지, method는 어떤 방식으로 보낼지를 설정한다.
- 그리고 파이썬의 데이터는 기본적으로 key:value로 이루어져 있는데, input에는 value만 넘겨 준다.
- 하지만 key가 정해져 있지 않은 value는 파이썬에서 다룰 수 없다.
- 이 key 역할을 하는 것이 input 프로퍼티 중 "name"이다.

```html
<!-- <!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>potato</title>
  </head>
  <body>
    <h1>Job Search</h1> -->
<form action="/result" method="get">
  <input name="word" type="text" placeholder="What job do you want" />
  <button type="submit">Search</button>
</form>
<!-- </body>
</html> -->
```

<br/>
- 이제 입력창에 값을 입력하고 버튼을 누르면 설정한 /result로 이동하게 된다.

<img src="/images/posts/flask_03.png">
<br/>
- 주소창을 자세히 보면 /result?word=감자 라고 나온다.
- url은 /result 까지이고 ? 이후는 result에 넘어간 데이터 값들이라고 이해하면 된다.
- 이 데이터들은 여러 값을 넣을 수 있고, "query arguments"라고 부른다.

### html에 데이터 주기

- 이제 서버에 전송된 값을 받아서 html에 보여주자.
- /result에 접속히 해당되는 html을 랜더링하고, 값을 html에 표시해주면 된다.
  <br/>
- 어떻게 표시해주지?
- 플라스크의 request 함수를 이요하면 된다!
- request는 웹사이트에 갈 때마다 서버가 특정 동작을 취하게끔 만들기 위해 클라이언트에서 전송하는 메시지이다.
- request를 통해서 리소스를 클라이언트로 받아 오는 것이다.
- 이 리소스 안에서 우리는 입력값 word, 즉 query arguments를 찾아 갖고 오면 된다.
- 아래 문법을 통해 값을 정의할 수 있다.

```python
word = request.args.get("word")
```

<br/>
- 자 이제, 값을 저장한 변수를 어떻게 html에 넘길까?
- 아주 간단하다. render_template함수에 값을 저장한 변수(word)를 html에 넘길 변수(search_word)에 저장하여 넘기면 된다.

```python
from flask import Flask, render_template, request

# app = Flask("appName")

# @app.route("/")
# def home():
#   return render_template("potato.html")

@app.route("/result")
def result():
  word = request.args.get("word")
  return render_template("result.html", search_word = word)

# app.run(host="0.0.0.0")
```

<br/>
- 이러면 서버에서 작업은 끝이다.
- html에선 어떻게 저 값을 표시할 수 있을까?
- search_word = word 은 word의 값을 search_word에 담아 전달하는 것이다.
- `{% raw %}{{search_word}}{% endraw %}` 로 표시하면 플라스크에서 html과 python을 보고 있다가 해당 문법을 인식하고 변수에 값을 전달해준다.

```html
<!-- <!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>result</title>
  </head> -->
<body>
  <h1>Search Results</h1>
  <h3>You are looking for "{{search_word}}"</h3>
</body>
<!-- </html> -->
```

### html a 앵커 요소를 이용하여 페이지 이동하기

- 이제 검색을 한 후, 다시 뒤로 돌아갈 수 있는 요소를 만들어 보자.
- 페이지를 이동할 때 쓰는 html 태그는 앵커 태그이다.
- 앵커 태그는 href를 기본적으로 사용하는데, 여기에 플라스크의 route에 쓴 것처럼 /로 시작하는 url 주소를 입력하면 된다.

```html
<!-- <!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>result</title>
  </head>
  <body>
    <h1>Search Results</h1>
    <h3>You are looking for {{search_word}}</h3> -->
<a href="/">뒤로 가기</a>
<!-- </body>
</html> -->
```

<br/>

### 이제 입력 값을 서버에 전송하고,

### 받는 것을 할 수 있으니 보고싶은 채용 공고의 키워드를 입력하여

### 채용 플랫폼 사이트에서 해당 단어와 관련된 정보를 크롤링하여

### 내가 구축한 환경에 뿌려보도록 하자!
