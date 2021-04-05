---
layout: post

title: 같은 디자인 버튼에 이벤트 리스너 달기 "#2"

tags: [javascript, frontend, blog, 반응형]

image:
---

<img src="/images/posts/javascript_logic_01.jpg">

```javascript
if(ul.className === "side-nav__ul second-menu"){
    for(let i = 0; i < hidden.length; i++){
      hidden[i].classList.toggle("none");
    }
    if(icon.className === "fas fa-chevron-down"){
      icon.className = "fas fa-chevron-up"
      title.innerText = "간략히 보기"
    } else{
      icon.className = "fas fa-chevron-down"
      title.innerText = "더보기"
    }
  } else if(ul.className === "side-nav__ul subscribe"){
    for(let i = 0; i < hidden.length; i++){
      hidden[i].classList.toggle("none");
    }
    if(icon.className === "fas fa-chevron-down"){
      icon.className = "fas fa-chevron-up"
      title.innerText = "간략히 보기"
    } else{
      icon.className = "fas fa-chevron-down"
      title.innerText = `${hidden.length}개 더보기`
    }
```

<br>
### 더보기 메뉴의 코드와 로직 첫 상태이다.
<br>
처음 로직을 그려서 코드를 짤 때는 일단 단순하게 생각하고 기능이 우선적으로 작동하도록 설계했다. <br>
그 후 다시 로직과 코드를 보며 중복되거나 불필요한 코드를 발견하고 이를 정리하는 과정을 진행했다. <br>
js코드가 돌아가는 로직을 그림으로 그렸더니 정리가 필요한 부분이 시각적으로 보여서 편리했다.

---

<img src="/images/posts/javascript_logic_02.jpg">

```javascript
for (let i = 0; i < hidden.length; i++) {
  hidden[i].classList.toggle("none");
}

if (ul.className === "side-nav__ul subscribe") {
  if (icon.className === "fas fa-chevron-down") {
    icon.className = "fas fa-chevron-up";
    title.innerText = "간략히 보기";
  } else {
    icon.className = "fas fa-chevron-down";
    title.innerText = `${hidden.length}개 더보기`;
  }
} else {
  icon.className = "fas fa-chevron-down";
  title.innerText = "더보기";
}
```

<br>
### 첫 리팩토링을 진행 후 코드 상태이다.
<br>
중복되는 for문과 if문을 지우고, 두 개의 버튼의 분기점을 아이콘 클래스 이름으로 바꿔 진행하였고 <br>
N개 더보기의 분기를 ul의 클래스네임으로 구분지었다.<br>
왜냐하면 2개의 더보기 버튼의 공통점은 화살표 아이콘이 동일하다는 것이고,<br>
차이점은 ul의 클래스이름을 다르게 지정한 점을 근거로 분기를 설정하였다.

---

<img src="/images/posts/javascript_logic_03.jpg">

```javascript
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
```

<br>
### 최종 코드 상태
<br>
if조건문 중 안과 밖을 바꿈으로써 감싸던 if문을 없앴다.<br>
한줄이라도 더 줄일 수 있는 방법이 더 없나 살펴보았지만, 이정도로 만족했다.
