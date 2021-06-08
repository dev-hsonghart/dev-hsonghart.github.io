---
layout: post

title: js- 화살표 함수(arrow function)

tags: [javascript]

image:
---

### arrow function

- 화살표 함수는 function 표현에 비해 구문이 짧다.
- 메소드 함수가 아닌 곳에 가장 적합하다. 그래서 생성자로서 사용할 수 없다.
- 화살표 함수에 return을 쓸 경우 중괄호{}는 생략된다.

### 기본 구문

- (argument) => 함수 내용
- 인자가 하나일 경우 괄호() 생략 가능
- 인자가 없을 경우 괄호() 사용 필요

```javascript
const btn = document.querySelector("button");

const handleClick = (event) => console.log(event);
btn.addEventListener("click", handleClick);
```

### 함수 패턴에서 짧은 함수가 환영받는다.

```javascript
const btn = document.querySelector("button");

// 001. function
function handleClick(e) {
  console.log(e);
}
btn.addEventListener("click", handleClick);

// 002. arrow function

const handleClick = (event) => console.log(event);
btn.addEventListener("click", handleClick);

// 003. arrow function

btn.addEventListener("click", (event) => console.log(event));
```
