---
layout: post

title: object를 활용하여 산수 함수 만들기

tags: [javascript, frontend, blog]

image:
---

챌린지 일지 Day3. 2021 03 10
벨로그에서 옮기는 중

---

### Object 선언

```javascript
const name = {
  name: hoho,
  age: 18,
};
```

name 이라는 오브젝트를 선언하였고, name의 name은 hoho이고, name의 age는 18이다.
라고 해석할 수 있다.

### 산수 함수 만들기

```javascript
const calculator = {
  plus: function (x, y) {
    return x + y;
  },
  minus: function (x, y) {
    return x - y;
  },
  multiply: function (x, y) {
    return x * y;
  },
  division: function (x, y) {
    return x / y;
  },
  percent: function (x, y) {
    return x % y;
  },
};

const plus = calculator.plus(5, 5);
console.log(plus); // 10

const minus = calculator.minus(5, 5);
console.log(minus); // 0

const multiply = calculator.multiply(5, 5);
console.log(multiply); // 25

const division = calculator.division(5, 5);
console.log(division); // 1

const percent = calculator.percent(5, 3);
console.log(percent); // 2
```
