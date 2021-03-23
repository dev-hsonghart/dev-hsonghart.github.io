---
layout: post

title: 이벤트와 이벤트 리스너

tags: [javascript, frontend, blog]

image:
---

챌린지 일지 Day3. 2021 03 10

---

> 자바스크립트는 html과 css를 바꾸는 기능을 하지만 이벤트에 반응하기 위해 만들어졌다.

## 이벤트란? 웹사이트에서 발생하는 것들을 말한다.

- click, resize, submit, input, change 등등등
- addEventListener

```javascript
function handleResize() {
  console.log("I have been resized");
}

//resize
window.addEventListener("resize", handleResize);
```

- handleResize를 할 때, 뒤에 ()를 붙이지 않는다. ()를 붙이면 함수가 이벤트가 일어나지 않아도 호출되기 때문이다.

## event.target

- 이벤트 리스너는 매개변수 event를 기본으로 가진다.
- event.target이란 해당 이벤트가 일어난 지점을 명칭한다.
- 자바스크립트로 html요소를 생성하여 이벤트리스너를 달았을 때 같은 요소가 많을 경우 target을 이용하여 해당 이벤트가 발생한 요소에만 함수가 호출될 수 있게 한다.

## querySelectorAll + for

- 이미 생성한 html요소를 querySelectorAll로 여러 개의 html 요소를 불러오면 배열로 저장이 된다.
- 이럴 때 for 반복문을 사용하여 조건에 맞는 요소가 함수가 실행되게 한다.

```javascript
const btnNum = document.querySelectorAll(".num");

for (let i = 0; i < btnNum.length; i++) {
  btnNum[i].addEventListener("click", displayValue);
}
```

- i 에 0을 선언한다.
- i가 btnNum 배열의 length보다 낮으면 아래 함수를 실행한 후 i에 1을 더한다. 이하 반복
- 해당 반복문은 i가 배열의 length를 넘어갔을 때 중지한다.
