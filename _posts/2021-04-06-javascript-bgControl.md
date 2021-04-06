---
layout: post

title: 배경 색상을 특정 값으로만 지정하기

tags: [javascript, frontend, blog, 반응형]

image:
---

<img src="/images/posts/javascript_bg_random.jpg">

<br>
### 중채도에서 고채도의 배경 색상으로만 추출하기
- 0 ~ 255 사이의 값이 랜덤하게 배정되면서 시각적인 문제를 발견하였다.
- 저채도의 색상이 추출될 때 화면이 어두워지고 칙칙해진다는 점이다.
- 이를 해결하기 위해 중채도 ~ 고채도의 색상값만 추출이 되게 수정하였다.

> RGB값의 중채도 ~ 고채도를 위한 필수 조건

1. RGB값은 3개의 값을 가지고 있다.
2. 3개의 값 중 0을 반드시 한 개 갖고 있어야 한다.
3. 나머지 2개의 값은 139 ~ 255 사이의 값이어야 한다.
   3.1 왜 139 ~ 255 사이여야 하는가? <br> 아래 스크린샷을 참고하자.

<img src="/images/posts/color_2.png">
<br>
<img src="/images/posts/color_1.png">
<br>
위 2개의 스크린샷은 rgb창에서 고채도일 때와 중채도 일때의 값일 때 화면이다. 나는 이 값을 기준으로 잡았다. 물론 이 값만으로 모든 중채도와 고채도를 표현할 순 없다.<br> 나는 단순히 저채도의 색상만은 나타나지 않았으면 하는 의도로 중채도 이상의 값을 정하여 진행하였다.

---

### 필요한 기능 정하기

- 위에 정의한 필수 조건을 만들 수 있는 기능을 정해보자.

1. RGB는 3개의 숫자를 가진 ARRAY이다.

```javascript
let rgb = [];
```

2. RGB는 0을 반드시 갖고 있어야한다.

```javascript
let rgb = [0, 0, 0];
```

3. 3개 중 2개만 139 ~ 255 사이의 값이 랜덤으로 들어가야 한다. <br>랜덤함수와 반복문이 필요하다.

```javascript
function randomRGB(array) {
  for (let i = 0; i < 2; i++) {
    array[i] = getRandomNum();
  }
  return array;
}

function getRandomNum() {
  return Math.floor(Math.random() * 256) + 139;
}
```

4. 다양한 색상을 표현하기 위해 랜덤값을 받은 ARRAY의 배열을 섞어주어야 한다.

```javascript
function shuffleArray(array) {
  for (let i = 0; i < array.length; i++) {
    let j = Math.floor(Math.random() * (i + 1));
    [array[i], array[j]] = [array[j], array[i]];
  }
  return array;
}
```

---

### 위 기능을 정리하여 나온 실행 코드이다.

```javascript
const bg = document.querySelector(".background-container");

let rgbA = [0, 0, 0],
  rgbB = [0, 0, 0];

function randomRGB(array) {
  for (let i = 0; i < 2; i++) {
    array[i] = getRandomNum();
  }
  return array;
}

function shuffleArray(array) {
  for (let i = 0; i < array.length; i++) {
    let j = Math.floor(Math.random() * (i + 1));
    [array[i], array[j]] = [array[j], array[i]];
  }
  return array;
}

function getRandomNum() {
  return Math.floor(Math.random() * 256) + 139;
}

function displayBg() {
  randomRGB(rgbA);
  randomRGB(rgbB);
  shuffleArray(rgbA);
  shuffleArray(rgbB);

  bg.style.background = `linear-gradient(to right, rgba(${rgbA[0]}, ${rgbA[1]}, ${rgbA[2]}), rgba(${rgbB[0]}, ${rgbB[1]}, ${rgbB[2]}))`;
  bg.style.opacity = 0;
}

function init() {
  displayBg();
  setInterval(displayBg, 30000);
}

init();
```

<br>
<strong>코드 풀이</strong><br>
- 그라데이션은 색상 인자를 시작점과 종료점으로 2개 받는다. 그래서 rgb array를 2개 선언하였다.
- 배열을 섞는 함수는 피셔 예이츠 알고리즘이 적용된 함수인데, 이 부분은 따로 공부해보기로 했다. 이 알고리즘은 셔플의 결과값이 비슷한 확률로 추출될 수 있다는 장점이 있다.

---

### 이슈 발견

- 위 코드대로 실행을 시킨 후 이슈가 발생했다.
- rgb의 조건 중 하나가 불일치된 것이다.
  > <strong>rgb값에 0이 없어지는 이슈</strong>
- 위 이슈는 셔플함수로 인해 3번째 자리에 값이 배정될 경우 이 3번째 값이 계속 유지가 되었다. 왜냐하면 랜덤함수는 3번째 자리에는 값을 배정하지 않기 때문이다.
- 위 이슈를 해결하기 위해 배열을 0으로 초기화 하는 함수를 만들어 추가하였다.

```javascript
function rgbInit() {
  rgbA = [0, 0, 0];
  rgbB = [0, 0, 0];
}
```

<br>
### 이렇게 해서 완성된 최종 코드이다.

```javascript
const bg = document.querySelector(".background-container");

let rgbA = [0, 0, 0],
  rgbB = [0, 0, 0];

function rgbInit() {
  rgbA = [0, 0, 0];
  rgbB = [0, 0, 0];
}

function randomRGB(array) {
  for (let i = 0; i < 2; i++) {
    array[i] = getRandomNum();
  }
  return array;
}

function shuffleArray(array) {
  for (let i = 0; i < array.length; i++) {
    let j = Math.floor(Math.random() * (i + 1));
    [array[i], array[j]] = [array[j], array[i]];
  }
  return array;
}

function getRandomNum() {
  return Math.floor(Math.random() * 256) + 139;
}

function displayBg() {
  rgbInit();
  randomRGB(rgbA);
  randomRGB(rgbB);
  shuffleArray(rgbA);
  shuffleArray(rgbB);

  bg.style.background = `linear-gradient(to right, rgba(${rgbA[0]}, ${rgbA[1]}, ${rgbA[2]}), rgba(${rgbB[0]}, ${rgbB[1]}, ${rgbB[2]}))`;
  bg.style.opacity = 0;
}

function init() {
  displayBg();
  setInterval(displayBg, 30000);
}

init();
```
