---
layout: post

title: 시계 만들기

tags: [javascript, frontend, blog]

image:
---

자바스크립트 챌린지 day5.
벨로그에서 옮기는 중

---

### 시간 다루기

- 아래 메소드를 이용해 현재 시간 정보를 가져온다.
- getHours() : 시간
- getMinutes() : 분
- getSeconds() : 초

```javascript
const timeContainer = document.querySelector("div");
timeText = timeContainer.querySelector("h1");

function getTime() {
  const date = new Date(), // Date()는 class 개념인데 나중에 다루도록 하자
    hours = date.getHours(),
    minutes = date.getMinutes(),
    seconds = date.getSeconds();

  timeText.innerText = `&{hours}:${minutes}:${seconds}`;
}

function init() {
  getTime();
}

init();
```

### setInterval

- 위 코드는 새로고침을 한 시점에만 시간을 불러온다.
- setInterval(함수, 1000); // 1000 = 1s
- 설정한 시간마다 함수를 실행하여 자동으로 시간을 불러옴

```javascript
function init() {
  getTime();
  setInterval(getTime, 1000);
}

init();
```

### mini if

- 한자리의 수와 두 자리 수의 자리수를 맞추기 위해 if를 사용하여 숫자 앞에 0을 추가함.

```javascript
if(hours < 10){
	timeText.innerText = `0${hours}`} else{
    timeText.innerText = `${hours}`}
    }
```

```javascript
hours < 10 ? `0${hours}` : hours;
```

- hours 가 10보다 작으면 hours 앞에 0을 붙이고 아니면 hours로 출력
- 일반 if()보다 간단하여 문장 안에 활용하기 좋다.

### 시간 차이 구하기

- D-day나 카운트다운에 활용

```javascript
const countDate = document.querySelector("span");

function xmasDDay() {
  const countTime = new Date("2021-12-24:00:00:00+0900");
  // 카운트다운 지정일을 선언
  const nowDate = new Date();
  // 현재를 선언
  const diff = (countTime.getTime() = nowDate.getTime());
  // 카운트다운 지정일과 현재의 시간 차이 구하기
  const diffDays = Math.floor(diff / (1000 * 60 * 60 * 24));
  // 결과값을 일수 단위로 바꾸기 + 소수점 버리기(Math.floor)
  span.innerHTML = diffDays < 10 ? `0${diffDays}일` : `${diffDays}일`;
  // 남은 날을 출력하기
}
```

> 크리스마스 이브 카운트 다운 만들기 결과물 : https://4r6g0.csb.app/
