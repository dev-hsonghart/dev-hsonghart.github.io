---
layout: post

title: filter 함수

tags: [javascript, frontend, blog, 모멘텀]

image:
---

### filter()

- 배열 정리 함수
- 배열을 순회하며 요소마다 조건 확인 후 조건문(callback)을 만족하는 요소들로 구성된 새로운 배열로 리턴시킨다.
- callback 에는 조건문이나 함수가 들어간다.

```javascript
let array = arr.filter(callback);
```

### ✍🏻 예시

```javascript
const cleanToDos = todos.filter(function (task) {
  // todos배열에 아래 조건에 맞는 것들을 모은다.
  return task.id !== backlogItem.id; // 매개변수의 아이디와 해당대상의 아이디가 다른 것들만 추리고 갖고 있는다.
});
todos = cleanToDos; // 투두스의 배열은 위에서 추린 배열과 같다.
saveToDo();
```

- 위 예시는 로컬스토리지에 저장된 배열형식에서 조건에 해당되는 요소들로 다시 리턴시킨다.
- 그 후 기존 배열에 저장시켜 로컬스토리지에 저장한다.

- 투두리스트에서 완료된 항목의 로컬스토리지 데이터를 다른 스토리지에 옮길 때 사용한 방식이다.
