---
layout: post

title: js- 자주 사용하는 array method

tags: [javascript]

image:
---

### 스프레드 문법

- Spread 는 우리말로 '펴다, 펼쳐지다' 의미를 가진다.
- 배열이나 문자열과 같은 반복 가능한(Iterable) 객체에 사용하여 객체 내부 데이터들을 펼쳐놓을 수 있다.
- 즉, array를 unpack 하여 item을 늘여놓을 수 있다.
- ...arrayName 을 사용하면 된다.

```javascript
const days = ["Mon", "Tue", "Wed"];
const otherDays = ["Thu", "Fri", "Sat"];
```

이 2개의 배열을 하나로 합치고 싶다.

```javascript
const days = ["Mon", "Tue", "Wed"];
const otherDays = ["Thu", "Fri", "Sat"];

const allDays = [...days, ...otherDays];

console.log(allDays); // ["Mon", "Tue", "Wed","Thu", "Fri", "Sat"]
```

<br/>

### map()

- 배열의 모든 아이템에 function을 실행하는 array의 method이다.
- 배열을 순회하면서 배열의 아이템에 callback 함수를 실행하고 실행결과를 모은 "새로운 배열"을 리턴한다.
- return 하지 않으면 아무 값도 없는 배열만 받게 된다.

```javascript
const days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];

const addSmile = (day) => `🙂 ${day}`;

const smileDays = days.map(addSmile);

console.log(smileDays); // ["🙂 Mon", "🙂 Tue", "🙂 Wed", "🙂 Thu", "🙂 Fri", "🙂 Sat"]
```

배열마다 이모지를 추가하여 새로운 배열(smileDays)을 만들어냈다.

### filter()

- 배열을 순회하며 각각의 아이템에 function 조건의 true에 해당되는 아이템만 모아서 배열을 리턴한다.

```javascript
const numbers = [2, 445, 6454, 22, 456, 23, 67, 11, 3, 4, 6, 3];

const testCondition = (number) => number > 15;

const biggerThan15 = numbers.filter(testCondition);

console.log(biggerThan15); // [445, 6454, 22, 456, 23, 67]
```

배열에서 15보다 큰 아이템만 모아서 새로운 배열(biggerThan15)에 저장하였다.

```javascript
let posts = ["Hi", "Hello", "Bye"];

const clean = (post) => post !== "Bye";

posts = posts.filter(clean);

console.log(posts); //["Hi", "Hello"]
```

배열에서 "Bye"가 아닌 아이템만 모아서 기존 배열에 저장하였다.
