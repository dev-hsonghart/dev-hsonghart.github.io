---
layout: post

title: 파이썬&플라스크- 채용 플랫폼 공고를 크롤링해서 html에 뿌려보자.

tags: [python]

image:
---

### 선택한 채용 플랫폼의 url 규칙을 살펴 보자.

- 내가 선택한 사이트는 [이 곳이다.](https://remoteok.io)
- 선택한 이유는 딱히 없다. 온라인으로 듣는 강의에서 제시해준 사이트 중 하나를 골랐을 뿐이다.!
- 해당 사이트로 접속하여 채용 공고를 검색했을 때 url 규칙을 살펴보도록 하자.
- 나는 검색어에 design을 입력해 보았다.

<img src="/images/posts/flask_05.png">
<br/>

- https://remoteok.io/remote-검색어-jobs 의 형태를 가진다.
- 그렇다면 검색어 자리에 입력한 값을 넣어서 request를 하면 된다는 것을 알 수 있다.
- 나는 해당 url을 만드는 함수를 먼저 만들었다.

```python
def make_url(word):
    remote_search_url = f"https://remoteok.io/remote-{word}-jobs"
    return remote_search_url
```

- 원하는 직군의 공고를 볼 수 있는 Url은 만들었다.
- 하지만 우리는 때로는 그 직군의 공고가 없는 화면을 받을 수도 있다.
- 그럴 경우 어떻게 나오는지 알아보자.
- 해당 사이트에서 아무 의미없는 단어를 입력했을 때 사이트는 아무런 반응을 하지 않는다.
- 그럼 url에 입력해보자.

<img src="/images/posts/flask_06.png">
url을 직접 입력했더니 사이트 상태값 중 404를 리턴한다.

<br/>

- 404는 에러로 인식한다. 그러므로 request를 할 때 try/except을 사용하여 404가 반환될 때 즉 = 채용 공고가 없을 경우를 처리해줘야 한다.

---

### 503 Service Unavailable

- 일단 아무 단어나 입력하여 해당 url을 requests 하였다.

```python
url = make_url()
res = requests.get(url)
print(res)
```

<img src="/images/posts/flask_07.png">
이런 응답을 뱉었다. 음..

- 보통은 200을 뱉어야 제대로 성공한 것이다. 이 상태로 soup으로 만들려고 해도 에러가 발생한다.
- 이럴 경우 요청할 때, header에 User-Agent또는 Referer를 지정하고 접근하면 해결 가능하다.

```python
headers = {
        "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.1916.47 Safari/537.36"
    }
url = make_url()
res = requests.get(url, headers=headers)
print(res)
```

<img src="/images/posts/flask_08.png">
<br/>

- 이제 200을 뱉는다. soup을 이용해 html을 긁어오자.

<br/>

```python
def make_url(word):
    remote_search_url = f"https://remoteok.io/remote-{word}-jobs"
    return remote_search_url


def find_jobs_list(word):
    url = make_url(word)
    headers = {
        "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.1916.47 Safari/537.36"
    }
    try:
        res = requests.get(url, headers=headers)
        html = BeautifulSoup(res.text, "html.parser")
        job_board = html.find("table", {"id": "jobsboard"})
        jobs_results = job_board.find_all("tr", {"class": "job"})
    except:
        jobs_results = None
    return jobs_results

```

<br/>

- try는 공고가 있을 경우 , except은 공고가 없을 경우로 진행하였다.
- 왜냐하면 공고가 없을 경우에 404을 반환하기 때문에 에러로 처리해야 한다.
- 공고의 조건에 맞는 element은 list형태로 저장되기에 except에서 list 값은 None 으로 저장하여 처리하였다.

---

### 긁어온 공고들을 딕셔너리로 분류하여 다시 list로 내보내자.

- html elements를 긁어왔기 때문에, 이것들 중 필요한 string만 뽑아내어 다시 정리할 필요가 있다.
- for 문을 사용하여 각 정보에 해당하는 요소를 뽑아 딕셔너리로 저장하고, 새로운 리스트에 추가하여 데이터를 만들자.

```python
def remoteok_find_jobs(word):
    job_list = []
    jobs_list = find_jobs_list(word)

    if jobs_list:
        for job in jobs_list:
            company_info = job.find("td", {"class": "company"})
            title = company_info.find("a").get_text()
            link = company_info.find("a")["href"]
            company = company_info.find("span").get_text()
            locate = company_info.find("div", {"class": "location"})
            if locate:
                locate = locate.string
            else:
                locate = "정보 없음"
            recruit_rate = job.find("td", {"class": "time"}).get_text()

            job_dict = {
                "title": title,
                "link": f"https://remoteok.io/{link}",
                "company": company.strip(),
                "locate": locate.strip(),
                "rate": recruit_rate.replace("\t", " "),
            }

            job_list.append(job_dict)

    return job_list
```

<br/>

- 제일 먼저 if로 html elements가 None인지 확인하고 값이 있을 경우에만 분류를 시작하게 만들었다.
- 중간에 locate의 경우 값이 없을 경우가 있어서 이 부분도 처리해주었다.
- replace() 함수를 사용하여 불필요한 string을 제거하고 딕셔너리에 저장하였다.

---

### 이제 이 데이터를 html에 전달하여 나타내보자.

```python

@app.route("/result")
def result():
    word = request.args.get("word")
    jobs = remoteok_find_jobs(word)

    return render_template("result.html", word=word, jobs=jobs)
```

<br/>

- 이전에 만들어놓은 result를 수정하였다.
- result 페이지를 렌더링할 때 앞페이지에서 입력한 값을 받아오고, jobs 에 채용사이트에서 찾아온 결과값들이 담긴 list를 담았다.
- 이제 이 두 값을 result.html에 넘겨준다.

```html
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Find your jobs-result</title>
  </head>
  <body>
    <header>
      <h1>니가 검색한 단어 : {{word}}</h1>
      <a href="/">뒤로 가기</a>
    </header>

    <main>
      {% if jobs:%} {% for job in jobs%}
      <div>
        <h3>{{job.title}}</h3>
        <a href="{{job.link}}">이동</a>
        <h4>{{job.company}}</h4>
        <h4>{{job.locate}}</h4>
        <h4>{{job_rate}}</h4>
        <hr />
      </div>
      {% endfor%} {% else: %}
      <div>결과가 없다</div>
      {% endif %}
    </main>
  </body>
</html>
```

<br/>

- 값을 표시할 땐 `{% raw %}{{}}{% endraw %}` 을 사용하면 되지만, list형태의 값을 `{% raw %}{{}}{% endraw %}`에 넣으면 list 그 자체가 나타나게 된다.
- 순차적으로 돌며 값을 뿌리기 위해 for를 사용하여야 한다.
- `{% raw %}{%%}{% endraw %}` 안에 실제 파이썬에서 쓰던 문법을 사용하면 플라스크가 인식하고 실행한다.
- `{% raw %} {% for %} {% endfor %}{% endraw %} ` 나 `{% raw %} {% if %}{% endif %}{% endraw %} `로 사용하면 된다. 그리고 반드시 endif, endfor로 끝맺음을 해줘야 한다.
- jobs가 값이 None일 경우에 표시하기 위에 if로 먼저 jobs이 있는지 없는지 분기를 설정하고 있을 경우메나 for를 실행하게 코드를 작성했다.

<img src="/images/posts/flask_09.png">
이렇게 결과물이 나오게 된다! 이제 css로 이쁘게 꾸미도록 하자.🎨
