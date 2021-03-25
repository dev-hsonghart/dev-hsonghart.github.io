---
layout: post

title: range값 실시간으로 표시

tags: [javascript, frontend, blog]

image: "/images/posts/range.png"
---

자바스크립트 챌린지 day9.
벨로그에서 옮기는 중

---

## 첫 코드

1. range의 value를 이용해서 불러오려 했으나 실패!
   range의 value는 리로드 시 셋팅되는 초기값이기 때문에 항상 고정이다.

2. range의 oninput을 사용했다.
   > [https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers/oninput](https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers/oninput)

- oninput은 range에 사용자의 입력을 얻을 때 실행된다.
- 이벤트 리스너와 비슷한 개념인 것 같다.
- oninput에 function을 넣으면 해당 function이 실행된다.

```javascript
const range = document.querySelector("#range"),
  result = document.querySelector(".result");

function handleInput(e) {
  result.innerHTML = `${e.target.value}`;
  // 이벤트 타겟의 value를 result 안에 뿌린다.
}

function init() {
  range.oninput = handleInput; // range에 입력이 들어가면 handleInput을 실행한다.
  result.innerText = `${range.value}`; // range의 초기 셋팅 값을 뿌려준다.
}

init();
```
