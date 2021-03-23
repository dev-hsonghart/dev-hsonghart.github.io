---
layout: post

title: 시간대별로 인사말을 랜덤하게 출력하기

tags: [javascript, frontend, blog, 모멘텀]

image:
---

### 인삿말 배열 선언

```javascript
const helloMorning = [
  "안녕하세요.🤘🏻",
  "좋은 아침이에요.",
  "오늘 점심은 뭘 먹나요?",
  "😴 아침은 늘 힘들어요.",
];
```

- 배열 안의 요소를 인덱스값으로 랜덤으로 출력해보자.

### Math.random() \* 10

- 0부터 10 사이에서 소수점을 포함한 숫자를 랜덤으로 뽑아낸다.

### 올림, 내림, 버림

- 배열의 인덱스는 정수이다. 그러므로 소수점을 없애는 함수가 필요하다.

- Math.ceil() -> 올림
- Math.floor() -> 내림
- Math.round() -> 반올림

```javascript
function randomHello(a) {
  return a[Math.floor(Math.random() * a.length)];
}
```

### new Date(), getHours()

- 이제 시간대를 설정해보자

```javascript
(currentTime = new date()), (hour = currentTime.getHours());
```

- currentTime 에 현재 시간을 저장한다.
- getHours는 시간을 가져온다.
- hours 는 currentTime의 시간을 저장한다.

### if()

- if문을 사용하여 시간대별로 다른 인삿말을 출력한다.

```javascript
const helloMorning = [
    "안녕하세요.🤘🏻",
    "좋은 아침이에요.",
    "오늘 점심은 뭘 먹나요?",
    "😴 아침은 늘 힘들어요.",
  ],
  helloDay = [
    "날이 좋으면 산책 어때요? 😉",
    "🍚 점심 먹어야죠!",
    "집안일하기 좋은 시간~🧹",
  ],
  helloEvening = [
    "저녁 드셨어요?",
    "뭘 하며 쉴까요? 👀",
    "12시 전엔 자야돼요!",
    "오늘 하루도 고생했어요. 👍",
  ],
  helloNight = [
    "🥱 시간이 늦었어요!",
    "이제 침대에서 쉴까요? 😉",
    "올빼미 같으니라구! 🌙",
    "내일은 뭘 먹고 싶어요?",
  ];

const displayHello = document.querySelector(".print-hello");

function printHello() {
  (currentTime = new Date()), (hour = currentTime.getHours());

  function randomHello(a) {
    // 배열안에서 랜덤 뽑기
    return a[Math.floor(Math.random() * a.length)];
  }

  if (hour >= 6 && hour < 12) {
    // 6~12 아침
    displayHello.innerText = randomHello(helloMorning);
  } else if (hour >= 12 && hour < 18) {
    // 12~18 점심
    displayHello.innerText = randomHello(helloDay);
  } else if (hour >= 18 && hour < 24) {
    // 18~24 저녁
    displayHello.innerText = randomHello(helloEvening);
  } else if (hour >= 0 && hour < 6) {
    // 00~6 새벽
    displayHello.innerText = randomHello(helloNight);
  }
  displayHello.style.animation = "fadeInOut 60s ease-out infinite";
}

printHello();
```
