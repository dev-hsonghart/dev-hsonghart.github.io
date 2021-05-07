---
layout: post

title: 파이썬-input(), strip(), split()

tags: [python]

image:
---

### 콘솔창에서 입력값을 받고 싶을 때

- input()을 통해 입력값을 받을 수 있다.

```python
input("입력하세요")
```

<img src="/images/posts/python_input_01.png">
<br/>

### 입력값을 여러개 받고 따로 저장하고 싶어!

- split()을 사용하면 입력값을 나눠 list형태로 저장할 수 있다.
- ()안에는 입력된 string을 기준으로 구분한다.
- ()의 기본값은 스페이스 한칸이다. 아무것도 넣지 않고 실행하면 스페이스를 기준으로 잘라서 list에 저장한다.

```python
x_list = input("여러 가지 입력하세요\n").split(",")
print(x_list)
```

<img src="/images/posts/python_input_02.png">
<br/>

### 사용자의 행동은 예측할 수 없어.. 입력값의 공백을 전부 지워서 받고 싶어.

- strip()을 사용하면 지정한 string을 기준으로 좌,우 공백을 지울 수 있다.
- strip()은 저장이 된 값에서 작동한다. input().strip()은 에러가 뜨니 주의!
- 그런데 글자 사이에 있는 공백은 지울 수 없으니 참고.

```python
x_list = input("여러 가지 입력하세요\n").split(",")
print(x_list)

y_list = []
for a in x_list:
  result = a.strip()
  y_list.append(result)

print(y_list)
```

<img src="/images/posts/python_input_03.png">
<br/>

### 공백을 지웠다고 끝이 아냐.

- split()을 통해 list로 값을 저장했기 때문에, strip()을 한 값을 list에 다시 저장할 필요가 있다.
- 그래야만 공백이 삭제된 입력값을 사용할 수 있다. 기존에 만들어진 list에 저장하지 않으면, list는 공백을 가진 값을 계속 들고있다.

```python
x_list = input("여러 가지 입력하세요\n").split(",")
print(x_list)

for i in range(len(x_list)):
  item = x_list[i]
  result = item.strip()
  x_list[i] = result

print(x_list)
```

> 주의사항: list의 요소가 int의 속성인 즉, 숫자일 경우 이 요소는 index값을 갖지 않아서 for i in range(len(list)) 에서 i로 호출이 되지 않아서 오류가 뜬다.
