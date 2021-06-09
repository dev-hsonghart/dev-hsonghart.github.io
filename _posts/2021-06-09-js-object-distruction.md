---
layout: post

title: js- 객체 디스트럭처링 할당

tags: [javascript]

image:
---

### 객체 디스트럭처링(Object Destructuring)

- 객체의 각 프로퍼티를 객체로부터 추출하여 1개 이상의 변수에 할당한다.
- 할당 기준은 프로퍼티 키 이다.
- 즉, 순서는 의미가 없으며 선언된 변수 이름 = 프로퍼티 키 여야 한다.

```javascript
const user = { firstName: Taeto, lastName: Po };

const firstName = user.firstName;
const lastName = user.lastName;

console.log(firstName, lastName); // Taeto Po
```

프로퍼티 키를 사용하여 변수에 할당한 경우

```javascript
const user = { firstName: Taeto, lastName: Po };

const { firstName, lastName } = user;

console.log(firstName, lastName);
```

객체 디스트럭처링으로 변수에 할당한 경우

```javascript
const user = { firstName: Taeto, lastName: Po };

// firstName 은 fn에, lastName은 ln에 할당된다.
const { firstName: fn, lastName: ln } = user;

console.log(fn, ln);
```

해당 프로퍼티 값을 다른 변수 명으로 할당하고 싶을 경우
