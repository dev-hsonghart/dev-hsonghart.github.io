---
layout: post

title: 같은 디자인 버튼에 이벤트 리스너 달기

tags: [javascript, frontend, blog, 반응형]

image:
---

### 같은 디자인이 2벌일 경우 버튼에 동일한 기능을 구현할 때

(feat. 유튜브 클론코딩)
<br>
반응형을 연습하려고 유튜브 홈화면을 클론코딩 중이다.
아래 화면은 실제 클론코딩 중인 내 결과물이다.

<img src="/images/posts/youtube_sidemenu_A.png">
<img src="/images/posts/youtube_sidemenu_B.png">

<br>
위 둘은 같아 보이지만 사실 다르다. <br>
좌측은 사이드메뉴가 기본적으로 펼쳐질 때의 디자인이고,
우측은 브라우저 사이즈가 작아져 사이드메뉴가 숨겨졌을 때 나타나는 디자인이다.
여기서 다룰 것은 <strong>[더보기]</strong> 버튼이다.

---

### ParentNode 와 classList.toggle

- 저 넷의 공통점은 html 구조가 같다는 것이다.
- 넷의 기능은 더보기를 누르면 숨겨진 메뉴가 보이고, 더보기의 텍스트가 [간략히 보기]로 바뀐다.
- [간략히 보기]의 기능은 누르면 숨겨진 메뉴가 안보이고, 버튼 텍스트가 [더보기]로 바뀐다.
- 이 2개의 기능을 비교했을 때 toggle의 기능으로 정리하였고, parentNode를 미리 선언하고 e.target으로 이벤트가 일어난 버튼이 속해있는 영역에만 메뉴가 발생하도록 하였다.
- 물론 복수의 클래스를 불러와서 이벤트 리스너를 설정할 때는 for반복문을 사용하였다.

```javascript
// 더보기를 누르면 감춰진 메뉴가 보이고 한번 더 누르면 보여진 메뉴가 숨겨진다.
const subscribeList = document.querySelectorAll(".subscribe"),
  noarmlMore = document.querySelectorAll(".normalMore"),
  subscribeMore = document.querySelectorAll(".subMore");

function toggleMenu(e) {
  const ul = e.target.parentNode.parentNode.parentNode,
    li = e.target.parentNode.parentNode,
    hidden = ul.querySelectorAll(".hidden"),
    icon = li.querySelector("i"),
    title = li.querySelector(".side-menu__title");

  for (let i = 0; i < hidden.length; i++) {
    hidden[i].classList.toggle("none");
  }

  if (icon.className === "fas fa-chevron-down") {
    icon.className = "fas fa-chevron-up";
    title.innerText = "간략히 보기";
  } else if (ul.className === "side-nav__ul subscribe") {
    icon.className = "fas fa-chevron-down";
    title.innerText = `${hidden.length}개 더보기`;
  } else {
    icon.className = "fas fa-chevron-down";
    title.innerText = "더보기";
  }
}

function init() {
  printCurrentSubscribe();

  for (let i = 0; i < noarmlMore.length; i++) {
    noarmlMore[i].addEventListener("click", toggleMenu);
  }
  for (let i = 0; i < subscribeMore.length; i++) {
    subscribeMore[i].addEventListener("click", toggleMenu);
  }
}

init();
```

<br>

### 숨겨진 메뉴 갯수 뿌리기

- 숨겨진 메뉴는 아마 서버에 저장된 데이터를 불러와서 append를 하는 게 맞을 것 같다.
- 일단 클론코딩 중이라 html에 직접 마크업을 미리 해놓은 것으로 연습하였다.
- 숨겨진 메뉴는 display: none처리가 미리 되어있고, hidden이라는 클래스가 추가 부여되어 있다.
- hidden 클래스를 전부 불러오면 array로 묶이는데 length를 사용하여 갯수를 표현하고 문자열에 조합하여 뿌려주었다.
- 찾아오는 hidden 은 어차피 같으므로, 둘 중 한 군데에서만 갯수를 계산하고, 양쪽에 각각 뿌려주었다.
- n개 더보기 메뉴를 누를 경우, display: none을 none이라는 클래스에 부여하여, 토글기능으로 none이 있으면 빼고, 없으면 붙이며 접었다 펼치는 기능을 구현하였다.

```javascript
function printCurrentSubscribe() {
  // 구독 카테고리에 숨겨진 구독채널 갯수 표시
  const subHiddenHidden = subscribeList[0],
    subHiddens0 = subHiddenHidden.querySelectorAll(".hidden"),
    title = subHiddenHidden.querySelector(".Nmore"),
    subHidden = subscribeList[1],
    title2 = subHidden.querySelector(".Nmore");

  title.innerText = `${subHiddens0.length}개 더보기`;
  title2.innerText = `${subHiddens0.length}개 더보기`;
}
```
