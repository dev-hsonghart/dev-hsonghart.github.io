---
layout: post

title: function 익히기

tags: [javascript, frontend, blog]

image:
---

![자바스크립트-day3-upload.png)

챌린지 일지. Day3. 2021 03 10

Real.it에서 실습.

벨로그에 작성된 일지를 옮기는 중.

---

### function 함수 - 기능

- 함수 정의와 실행.

  ```javascript
  function sayHello() {
    console.log("hello");
  }

  sayHello(); // hello
  ```

- argument (인자) : 함수 내에서 쓰이는 변수. 외부 혹은 다른 함수에 사용된 데이터를 연결해 주는 역할.

  ```javascript
  function sayHello(potato, coke) {
    console.log("hello!", potato, "Im", coke);
  }

  sayHello("mary", "Tom"); // hello!mary ImTom
  ```

- 백틱 (``)을 사용하여 문장을 가독성 있게 표현할 수 있다.

  ```javascript
  function sayHello(potato, coke) {
    console.log(`hello! ${potato}. Im ${coke}`);
  }

  sayHello("mary", "Tom"); // hello! mary Im Tom
  ```

- return : 함수가 실행하여 얻은 값을 함수가 갖고 있게 하는 역할. (보통 함수는 실행되면 바로 어딘가로 전달한다.)

  ```javascript
  function sayHello(potato, coke) {
    return `hello! ${potato}. Im ${coke}`;
  }

  const helloName = sayHello("mary", "Tom");
  console.log(helloName); // hello! mary Im Tom
  ```
