---
layout: post

title: js-matchMedia

tags: [javascript, frontend, blog, 반응형]

image:
---

### matchMedia()

- css의 미디어쿼리처럼 반응형을 구현할 때 사용한다.
- css 속성이 바뀌는 것이 아닌 hmtl요소의 제어가 필요하여서 미디어쿼리 대신 사용하였다.
- `window.matchMedia("css 미디어쿼리 문법")`

### media , matches

- matchMedia 함수는 `media`와 `matches`라는 두 프로퍼티가 존재한다.
- media : 사용한 미디어쿼리 문자열을 반환
- matches : 현재 화면에 미디어쿼리의 범위에 들어가면 `true` , 아니면 `false`를 반환

```javascript
if (window.matchMedia("(min-width: 1024px)").matches) {
  // 1024px 이상일 때
} else {
  // 1024px 미만일 때
}
```

<br/>

### 실시간으로 브라우저 사이즈를 감지하진 않는다.

- 사이트 진입 시 한번만 호출되기 때문에 브라우저창을 줄일 때는 적용이 안된다.
- `resize` 이벤트와 묶어서 처리해야 해상도에 따라 반응하는 웹을 만들 수 있다.

```javascript
function mediaQueryNav() {
  // screen < 450px 일 때 gnbCenter에 display에 none 추가 , 우측 mic와 search에 display에 빈값을 준다.
  // 우측 mic와 search는 display 기본값이 none이다.
  const branchWidth = window.matchMedia("(max-width: 450px)");
  if (branchWidth.matches === true) {
    //450px 미만
    gnbCenter.style.display = "none";
    rightMic.style.display = "";
    rightSearch.style.display = "";
  } else {
    gnbCenter.style.display = "";
    rightMic.style.display = "none";
    rightSearch.style.display = "none";
  }
}

function init() {
  window.addEventListener("resize", mediaQueryNav);
}
init();
```
