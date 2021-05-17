---
layout: post

title: 파이썬-웹 크롤링을 하자

tags: [python]

image:
---

### 웹 크롤링이란?

- 웹상의 다양한 정보를 자동으로 검색하여 필요한 데이터를 추출하는 행위.
- Web 크롤링, 스크래핑(scraping)이라고도 한다.

### 어떻게 크롤링을 하는가?

- 보통 웹 크롤러를 사용하여 웹문서 복사본을 생성한 후 html에서 찾고자 하는 element 요소를 검색하여 데이터를 수집한다.

### 웹 문서는 어떻게 가져오지?

- 시작하기 전에 requests와 beautifulsoup4 이라는 패키지를 설치하고 그 안에 있는 모듈을 사용하여야한다.
- requests 모듈을 사용하여 url을 호출한 후, beautifulsoup 함수를 이용하여 html 웹 문서 형태로 변환하여 가져온다.

```python
import requests
from bs4 import BeautifulSoup

get_url = requests.get("HTTPS://www.naver.com")
get_html = BeautifulSoup(get_url.text, "html.parser")
print(get_html) # 웹 문서 전체가 console 창에 출력됩니다.
```

<br/>
### 가져오고 싶은 데이터를 긁어 오자.

- 만약 웹 페이지 내 모든 링크를 가져오고 싶다면?
- find / find_all 함수를 사용하여 원하는 태그 이름과 속성을 설정하여 변수에 저장하고 print 해보자.
- find("html element", {"attribute" : "value"}) or find_all
- find는 element 요소 중 첫번째 요소만 가져온다. (js에서 queryselector와 동일)
- find_all은 모-든 element 요소를 모아서 "list"형태로 만들어 반환한다.

```python
# import requests
# from bs4 import BeautifulSoup

# get_url = requests.get("HTTPS://www.naver.com")
# get_html = BeautifulSoup(get_url.text, "html.parser")

all_link = get_html.find_all("a")
print(all_link)
```

<br/>

### 갖고 온 요소는 어떻게 활용할까?

- 요소는 html태그를 포함한 코드 형태이다. 하지만 내가 사용하고 싶은 것은 태그가 품고 있는 content 요소 즉, text 이다.
- get_text()나 string 함수를 사용하여 string만 뽑아내면 된다.
- 하지만 요소는 list 형태로 저장되기 때문에, 반복문을 사용하여 각 요소를 돌면서 string만 추출하게 코드를 작성한다.
- for item in list:

```python
# import os
# import requests
# from bs4 import BeautifulSoup

# get_url = requests.get("HTTPS://www.naver.com")
# get_html = BeautifulSoup(get_url.text, "html.parser")
# all_link = get_html.find_all("a")

for item in all_link:
  item = item.get_text()
  print(item)
```

<br/>

### .get_text() 와 .string의 차이는?

- get_text()를 이용하면 지정된 html요소 내 모든 텍스트를 추출할 수 있다.
- 현재 태그를 포함하여 모든 하위 태그를 "제거"한 후 유니코드 텍스트만 들어있는 문자열을 반환한다.
- 모든 태그의 텍스트를 합하여 문자열로 반환하기 때문에, 마지막 태그에 사용하는 것이 좋다.

---

- string은 get_text()와 반대로 해당 태그 내의 문자열을 반환한다.
- 현재 태그 내 자식이 둘 이상일 경우, 무엇을 반환해야할 지 명확하지 않기 때문에 None을 반환한다.
- 하지만 자식이 하나이고 string 값을 가지고 있다면 자식의 문자열을 반환한다.
- 정확한 파싱은 string을 사용하는 것이 좋다.
