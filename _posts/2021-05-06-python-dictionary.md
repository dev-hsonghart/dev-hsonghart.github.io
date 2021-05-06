---
layout: post

title: 파이썬-딕셔너리-CRUD

tags: [python]

image:
---

### 딕셔너리-Dictionary

- 딕셔너리는 {}로 감싸고 있고, key:value 형태의 데이터로 이루어진 자료 구조이다.

### 딕셔너리 생성하기

- javascript에서 array를 생성하는 것처럼, {} 를 이용해 빈 딕셔너리를 생성할 수 있다.

```python
my_dict = {}
my_favorite_dict = {food:potato}
```

<br/>
### 딕셔너리에서 key가 있는지 찾기

- 딕셔너리 안에 key를 추가하기 전에 해당 key가 존재하는지 여부를 알아야한다. 그렇지않으면 기존 key가 갖고있는 value에 의도치 않게 덮어씌워 데이터를 업데이트해버린다.

- x in dict 을 사용하면, x가 있으면 True / 없으면 False를 반환한다. if를 활용하여 있으면 추가하지않고, 없으면 추가하는 간단한 로직을 짜보자.
- x not in dict 로 반대의 의미로 같은 로직을 사용할 수 있으므로, 편한 방법대로 사용하면 된다.

```python
def add_to_dict(x_dict, key="", value=""):
  if key in x_dict:
    print("이건 이미 있어")
  else:
    print("이건 추가할 수 있어")
```

<br/>
### 딕셔너리에 추가하기

- 아래 문법을 통해 딕셔너리에 추가할 수 있다.
- x는 key에 들어가는 값 / y는 value에 들어갈 값이다.
- dict[x] = y

```python
def add_to_dict(x_dict, key="", value=""):
  if key in x_dict:
    print("이건 이미 있어")
  else:
    x_dict[key] = value
```

<br/>

### 딕셔너리 기존 요소에 업데이트하기

- 이제 나는 딕셔너리 key값을 새로운 데이터로 업데이트하고 싶어졌다.
- 그렇다면 해당 Key가 있는지 확인 후, 없으면 추가 있으면 업데이트를 하면 된다.

- dict.update({x:y})의 문법을 사용한다. 이럴 경우 여러 값을 업데이트할 수 있다.

```python
def update_word(x_dict, key="", value=""):
  if key in x_dict:
    add_to_dict(my_favorit_dict, key, value)
  else:
    x_dict.update({key: value})
    // or //
    x_dict[key] = value // 키로 접근하여 단일 데이터 업데이트

update_word(my_favorit_dict, food, tomato)
```

<br/>

### 딕셔너리 기존 요소 삭제하기

- 딕셔너리에 이미 있는 요소를 삭제하고 싶어졌다.
- 위와 마찬가지로 지우고 싶은 key가 있으면 삭제, 없으면 해당 키는 없다는 문구를 출력해보자.
- 삭제 문법은 del dict[x] 이다.
- key를 삭제하면 할당된 value도 같이 삭제되기 때문에 인자는 key만 받아도 된다.

```python
def del_word(x_dict, key=""):
  if key in x_dict:
    del x_dict[key]
  else:
    print("이건 값이 이미 없어")
```
