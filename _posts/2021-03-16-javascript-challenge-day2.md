---
layout: post

title: Access main program. Access main security. Access main program grid

tags: [자바스크립트, 챌린지]

image: "/images/posts/1.jpg"
---

챌린지 일지. Day2. 2021.03.09

repl.it에서 실습

---

> 자바스크립트는 위에서 아래로 실행한다!

### 변수 사용

1. Create (생성)
2. Initialize (초기화)
3. Use (사용)

예시.

```javascript
let a = 111;
let b = a - 10;
a = 4;
console.log(b, a);
```

- let으로 a 를 생성
- a = 111 -> 초기화
- a - 10 -> 사용

변수 앞에는 let으로 시작하여 선언을 한다.

let은 생성하거나 초기화할 때 사용하고 변수 업데이트 시 사용하지 않는다.

let은 변경이 가능한 변수.

---

### 상수 사용

- const으로 시작하여 선언을 함
- const는 변경이 불가능.
- 변수를 선언할 때는 const로 먼저 선언하고, 정말 필요 시에만 let을 사용한다. 왜냐하면 가독성이 높아지기 때문.

```javascript
const a = 111;
let b = a - 10;
a = 4; //error
console.log(b, a);
```

**콤마(,)로 구분하여 let과 const 하나에 여러 개의 변수를 선언할 수 있다.**

> //~~ , /~~/ : 주석처리. 사용자의 메모, 부연 설명 등을 써놓은 코멘트, 코드로 인식하지 않는다. command + /

---

### 데이터 타입

1. string = text / "" 따옴표 , ' ' 안에 들어가는 데이터이고 문자를 표현
2. Boolean = true or false / 참과 거짓
3. number / 숫자
4. float / 소숫점 숫자

---

### 데이터 정렬

> 상수, 변수, 데이터 타입 모두 사용 가능.

1. Array = [ ]

- 여러 타입을 리스트 형식으로 정렬.
- DB에서 가져온 리스트 데이터일 경우 사용.
- 안에 데이터를 입력
- array의 첫번째를 불러오고 싶을 경우 = 0 으로 호출.
- object, array를 array 안에 저장가능.

```javascript
const daysOfWeek = ["Mon", "Tue", "Wed", "Thu", "Fri", 111, true, a];
```

> 문법 규칙 Camel case : 소문자로 시작하여 스페이스 대신 대문자로 입력. \*협업을 위한 약속

2. Object = { }

- 데이터들을 합쳐서 만들어야 할 경우 사용
- 각 값(value)에 이름(key)를 줄 수 있음.
- { }안에 입력
- object안에 array, object 저장 가능

```javascript
const whoAmI = {
  name: "HSH",
  age: 33,
  gender: "Female",
  favMovies: ["MARS", "Avengers", "Kingdom"],
};

console.log(whoAmI);

whoAmI.name = "HSH0404";

console.log(whoAmI.name);
```

> object 안의 값은 변경할 수 있다.

---

### 항상 신경써야 할 점

- 오타
- close를 제대로 하였는가?
- 콤마 (,)를 찍었는가?
