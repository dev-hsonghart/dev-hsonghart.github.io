---
layout: post

title: 파이썬- url의 상태값을 체크해보자.

tags: [python]

image:
---

### 원격으로 url의 상태가 온라인인지 아니면 어떤 문제가 생겨 다운이 됐는지를 체크해보고 싶다.

- 모듈을 이용하여 url의 상태를 체크해볼 수 있다.

```python
import requests
from urllib.request import urlopen
```

<br/>

### 입력한 url이 형식에 맞는지 부터 체크해야 한다.

- 사용자가 url에 맞는 형식을 입력하지 않을 경우가 있다. 이유는.. 사용자 맘이다.
- 그러므로 제일 첫 분기는 web주소인지 아닌지를 파악해야 한다.
- web에는 .com , .co.kr 등으로 끝나는데 이 점에 대한 공통점은 `.`이 항상 들어간다는 점이다.
- 입력값에 `.`이 있는지 먼저 체크해보자.
- 콘솔창에 입력값을 받을 수 있는 함수는 input()이고, 기본값은 빈값이다.
- string 안에서 특정 요소를 찾는 함수는 find 이다. 해당 요소가 있으면 그 요소의 위치를 반환하고, 없을 경우 -1을 반환한다.

```python
# import requests
# from urllib.request import urlopen

def url_check():
  url_input = input()
  res = urlopen(url_input)

  if url_input.find(".") != -1:
    print(res)
  else:
    print("정상적인 web 주소가 아닙니다.\n")
url_check()

```

<br/>

### 입력을 제대로 안했다면 다시 입력 기회를 주고 싶다.

- 사용자가 잘못된 입력값을 입력했을 경우, 다시 입력 기회를 주고 싶다면
- while을 사용하여 다시 첫 순서로 돌리면 된다.
- while은 반복문인데 for와는 다르게 사용된다.
- for : 반복횟수가 정해진 경우. 주로 배열(list)과 함께 사용
- while : 무한 루프나 특정 조건에 만족할 때까지 반복 사용. 주로 파일을 읽고 쓰기에 사용된다.

```python
# import requests
# from urllib.request import urlopen

def url_check():
  while True:
    # url_input = input()
    # res = urlopen(url_input)

    # if url_input.find(".") != -1:
    #   print(res)
      break
    # else:
    #   print("정상적인 web 주소가 아닙니다.\n")
# url_check()
```

- 사용자가 url 입력을 제대로 할 경우 url을 불러오고 끝날 것(break)이고, 입력값을 제대로 안한 경우엔 제대로 입력할 때까지 while문 안에 있는 기능(input)을 반복할 것이다.

<br/>

### url의 상태값을 알고 싶다.

- urlopen함수를 이용하여 가져온 값은 입력한 http url과 관련된 인터넷 리소스이다.
- 상태값은 status로 가져올 수 있는데 한번 시도해보자

```python
  # while True:
  #   url_input = input()
  #   res = urlopen(url_input)

  #   if url_input.find(".") != -1:
      print(res.status)
#       break
#     else:
#       print("정상적인 web 주소가 아닙니다.\n")
# url_check()

```

<br/>

- 시도한 순간 콘솔창에는 뻘건 에러 메시지가 뜰것이다.
  <br/>
  <img src="/images/posts/python_http_error.png">
  아 너무 무섭다..

- 우리는 에러를 읽을 때 마지막 줄 부터 거꾸로 타고 올라가는 버릇을 들여야한다! (에러가 나는 주 원인은 마지막 줄이다!)

```python
ValueError: unknown url type: 'www.naver.com'
```

- 에러의 의미는 입력한 url이 알수 없다는 것이다.
- 분명 .com도 있고 www도 있는데, 무엇이 빠진걸까?
- urlopen은 "http" url과 관련되어 있다고 써있다.
- 많은 사용자들은 www부터 쓰는 것이 보편적이다. 그러면 우리는 https:// 가 없을 경우엔 이 string을 넣어 url에 담아 리소스를 요청해야한다는 것이다.

```python
# import requests
# from urllib.request import urlopen

# def url_check():
#   while True:
#     url_input = input()
#     host = "https://"

#     if url_input.find(".") != -1:
      if url_input.find(host) == -1:
        url_input = "https://" + url_input
        res = urlopen(url_input)
        print(res.status)
      else:
        res = urlopen(url_input)
        print(res.status)
#       break

#     else:
#       print("정상적인 web 주소가 아닙니다.\n")

# url_check()
```

<img src="/images/posts/python_http_status.png">

- 이제 제대로 에러없이 작동이 되는 모습이다.
- status는 사이트 상태에 따라 200과 같은 숫자를 반환한다.
- [상태값은 이 문서를 참고하자. ](https://developer.mozilla.org/ko/docs/Web/HTTP/Status)

### 만약 없는 주소를 입력할 경우 어떻게 되지?

- 해당 사이트의 서버가 내려갔거나 아예 존재하지 않는 url일 경우
- 우리가 흔히 보는 "404 Not Found"를 돌려준다.
- 그리고 우리는 또 긴긴 에러 메시지를 콘솔에서 볼 수 있다(아 너무 두렵다.)

<img src="/images/posts/python_http_error_1.png">

- 침착하게 에러를 읽어보자.
- 음.. 서비스 낫 노운.. 대충 서비스가 없다는 것 같다.
- 에러 예외 처리가 필요한 순간이다!
- 이럴 때 우리는 try와 except 를 사용하여 이와 같은 경우를 처리할 수 있다.

### Try. Except

- try 와 except 은 단어 그대로의 뜻이다.
- 시도하고 예외한다.
- try 안에 있는 코드를 우선 시도하고, 그게 맞으면 계속 진행. 아니면 except 코드를 실행한다.

```python
# import requests
# from urllib.request import urlopen

# def url_check():
#   while True:
#     url_input = input()
#     host = "https://"

#     if url_input.find(".") != -1:
#       if url_input.find(host) == -1:
#         url_input = "https://" + url_input
        try:
            res = urlopen(url_input)
            if res.status == 200:
              print(f"{url_input}은 작동중")
            break
        except:
            print(f"{url_input}은 없는 주소\n") ## 404
#       else:
#         res = urlopen(url_input)
#         print(res.status)

#     else:
#       print("정상적인 web 주소가 아닙니다.\n")

# url_check()
```

<img src="/images/posts/python_http_success.png">

- 이제 입력한 url 상태를 예외처리하여 정상적으로 찾아오고 있다.
- while의 break는 작동하는 사이트를 찾았을 경우에만 실행이 되게 위치를 다시 옮겨 주었다.
- url 형식으로 입력하지 않거나, 입력한 Url이 존재하지 않을 경우엔 다른 주소를 입력할 수 있게 로직을 짰다.
