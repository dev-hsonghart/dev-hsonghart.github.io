---
layout: post

title: 파이썬&플라스크- csv로 내보내기 + 임시 DB를 생성하여 사용성을 올리자.

tags: [python]

image:
---

### DB 생성

- DB란 데이터베이스(DataBase)의 약자이다.
- 정보를 체계적으로 축적하여 특정 다수의 이용자들에게 필요한 정보를 제공하는 역할을 한다.
- 일반적으로 소프트웨어와는 별개의 공간에서 관리하지만, dictionary형태로 임시 DB를 만들어 이미 한번 검색했던 공고를 다시 검색할 경우엔 DB에 있는 데이터를 바로 갖고와서 뿌려줌으로써 사용성을 올릴 수 있다.

```python
DB = {}
# 임시 DB 생성
```

### if문을 사용하여 DB에 있는 공고 정보를 Create, Read한다.

- 사용자가 입력한 공고 키워드 값을 통해 해당 key가 DB에 있을 경우, 스크리퍼를 실행하지 않는다.
- key가 DB에 없는 경우, 스크리퍼를 실행하여 공고 데이터를 가져온 후 DB에 해당 Key와 value로 구성하여 저장한다.

```python
@app.route("/result")
def result():
    word = request.args.get("word")
    fromDB = DB.get(word)

    if fromDB:
        jobs = fromDB
    else:
        jobs = find_jobs_list(word)
        DB[word] = jobs

    return render_template("result.html", word=word, jobs=jobs)
```

### csv

- csv란 Comma-separated values의 약자로서 각 라인의 컬럼들이 콤마로 분리된 텍스트 파일 포맷이다.
- csv 파일을 만지기 위해선 파이썬에 기본 내장된 csv 모듈을 import 해줘야 한다.

```python
import csv
```

### csv 파일 읽기

- .csv 파일을 오픈한다.
- 파일객체를 csv.reader(파일객체)에 넣으면 된다.
- csv.reader() 함수는 for루프를 돌며 한 라인씩 가져올 수 있다.
- 이때 반환되는 라인은 컬럼들을 나열한 리스트(list) 타입이다.

```python
import csv

file = open("data.csv", "r", encoding="utf-8")
read_column = csv.reader(file)
for line in read_column:
  print(line)
file.close()
```

위 코드는 실제 실습에서 사용하지 않은 예시 코드이다.

### csv 파일 만들기

- 스크리퍼에서 긁어온 정보들을 csv 파일로 만들어보자.
- csv파일로 만드는 이유는 사용자가 해당 정보들을 편하게 확인하기 위해 csv파일을 다운받을 수 있는 기능을 위함힝다.
- csv 만들기 역시 read와 마찬가지로 wirter()함수를 이용하여 만들면 된다.
- if조건문에는 jobs 즉, 채용 공고 정보가 있을 경우에만 실행하는 함수로 만든다.
- 검색 키워드로 나오는 정보들이 없을 경우엔 csv 다운로드 기능을 제공할 필요가 없기 때문이다.
- csv writer는 writerow()를 통해 새로운 line을 추가한다.
- for문을 이용해서 각 채용 정보들의 value값들만 뽑아서 라인에 추가하도록 작성한다.

```python
def save_csv(jobs, word):
    if jobs:
        file = open(f"{word}.csv", "w")
        writer = csv.writer(file)
        writer.writerow(["title", "link", "company", "locate", "date"])
        for job in jobs:
            writer.writerow(job.values())
```

### csv 내보내기 = 다운로드

- csv파일을 내보내는 기능을 사용하려면 flask 모듈에서 `send_file`을 import해준다.
- 로직은 간단히 이렇다

1. 검색 결과가 1개 이상일 경우에만 csv를 내보낼 수 있다.
2. csv 내보내기는 a 태그의 href로 특정 Html로 해당 검색어 값을 같이 넘겨 save_csv함수를 작동시킨다.
3. 생성된 csv를 send_file()를 실행하여 해당 검색어 값을 이름으로 가진 csv파일로 내보낸다.

```html
<header>
  <!-- <h1>니가 검색한 단어 : {{word}}</h1>
      <a href="/">뒤로 가기</a> -->
  {% if jobs:%}
  <a class="result_export_csv" href="/export?word={{word}}" target="_blank"
    >Download csv</a
  >
  {% else:%}
  <a class="hidden" href="/" target="_blank"> </a>
  {% endif %}
</header>
<!-- 
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
</main> -->
```

```python
@app.route("/export")
def export_csv():
  word = request.args.get("word")
  jobs = DB.get(word)
  save_csv(jobs, word)
  return send_file(f"{word}.csv", mimetype="application/x-csv",attachment_filename=f"{word}.csv", as_attachment = True)
```

### 이렇게 특정 검색어에 맞는 정보를 가져오고,

### 해당 결과값들을 정리하여 파일로 내보내는 잡 스크리퍼를

### python으로 만들어 보았다.
