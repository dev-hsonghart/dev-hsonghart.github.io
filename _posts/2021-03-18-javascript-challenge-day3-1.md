---
layout: post

title: Dom

tags: [javascript, frontend, blog]

image:
---

챌린지 일지 Day3. 2021 03 10
벨로그에서 옮기는 중

---

### DOM = document Object Model

- html을 객체(object)로 가져와 자바스크립트에서 활용할 수 있게 해준다.

---

### HTML과 자바스크립트를 함께 쓰려면 어떻게 해야할까?

1. html과 css를 먼저 떠올려보자.

- 우리는 html 에서 tag를 입력한다.

```html
<div id="text">Hi</div>
```

- 그리고 div에 해당되는 컬러를 모두 변경하고 싶어졌다.
- 그러려면 css에서 변경하고 싶은 html 태그를 불러와야 한다.
- css로 들어가 div에 할당된 id를 불러온다.

```css
#text: {
  color: white;
  background-color: black;
}
```

- 이러면 html에 있는 "Hi"의 컬러가 변경된다.
- 이와 같이 자바스크립트에서도 html의 div태그를 자바스크립트에서 다룰 수 있게 불러와야 한다.
- 그걸 DOM을 통해 할 수 있다.

```javascript
const text = document.getElementById("text"); // html에서 "text"라는 id를 가진 요소를 불러와서 상수 text에 저장하였다.
console.log(text); // 상수 text를 띄운다.
```

### document.querySelector()

- queryselector는 특정 name이나 id를 제한하지 않고 css선택자와 동일하게 요소를 찾을 수 있다.
- id : #id
- class : .class
- html : tag
