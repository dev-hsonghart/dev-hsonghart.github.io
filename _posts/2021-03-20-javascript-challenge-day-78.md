---
layout: post

title: 투두리스트 만들기

tags: [javascript, frontend, blog]

image:
---

자바스크립트 챌린지 day7~8.
벨로그에서 옮기는 중

---

## 1. Form에 이벤트 리스너를 달고, input.value를 화면에 뿌린다.

- li 요소를 자바스크립트로 생성하기 위해 기본적인 화면에는 li를 만들어두지 않으며, 생성할 위치를 미리 설계한다.
- form에 이벤트를 달아야하는데 input에 submit이벤트는 작동하지 않으므로 꼭 form에 submit 이벤트를 달아야한다.

```javascript
function init() {
  addForm.addEventListener("submit", function (e) {
    e.preventDefault();
    const currentValue = addInput.value;
    if (currentValue !== "") {
      paintPending(currentValue);
      addInput.value = "";
    }
  });
}
```

## 2. paint 함수 정의

- document.createElement 이용하여 html요소를 생성하는 기능을 상수에 담을 수 있다.
- button과 li을 정의하고 appendChild로 "어느 부모"밑에 넣을 것인지 정한다.
- li 와 button 이 생성된 부모 요소도 "어느 조부모" 밑에 넣을 것인지 정한다. (이 때 조부모는 이미 html에 생성된 요소이다.)

```javascript
const item = document.createElement("li");
// item은 li요소를 생성한다.
const itemText = document.createElement("span");
// itemText는 span요소를 생성한다.

const list = document.querySeletor("ul");
// list는 ul요소이다.

item.appendChild(itemText);
//item안에 itemText를 자식으로 생성한다.

list.appendChild(item);
//list안에 item을 자식으로 생성한다.

//** in HTML **//

<ul>
  <li>
    <span></span>
  </li>
</ul>;
```

## 3. list의 내용을 obj로 저장하여 로컬스토리지에 저장

- 노마드코드의 강의에서 newId를 선언할 때 배열.length + 1로 알려주었지만, 화면을 새로고침할 경우 각 2개의 스토리지 안 객체 id값이 동일해지는 현상이 나타난다. 그래서 랜덤함수를 사용한다.
- id와 text를 obj에 넣은 후, 넣고 싶은 로컬스토리지 key값에 push한다.
- 로컬스토리지 key값은 미리 빈 배열[]로 정의해놓는다.
- 이 때, 로컬스토리지를 set하여야 새로고침에도 사라지지 않는다.

> 로컬 스토리지에 저장할 땐 데이터타입이 자동으로 string이 되지만, 객체를 저장할 땐 그렇지 않기 때문에 string으로 변환해주는 JSON을 사용하여 set한다.
> localStorage.setItem(LCALDATA, JSON.stringify(localdata));

```javascript
function paintList(text) {
  const item = document.createElement("li");
  const itemText = document.createElement("span");
  itemText.innerText = text;

  const remove = document.createElement("button");
  remove.innerText = "❌";

  const checked = document.createElement("button");
  checked.innerText = "✅";

  checked.addEventListener("click", moveItme);

  item.appendChild(itemText);
  item.appendChild(remove);
  item.appendChild(checked);

  pendingList.appendChild(item);
  const newId = Math.random().toString(36).substr(2, 16);
  item.id = newID;

  const listObj = {
    id: newId,
    text: text,
  };
  pendingData.push(listObj);
}

function paintPending(text) {
  paindList(text);
  savePending();
}
```

## 4. 버튼을 통해 두 개의 메뉴로 이동시키기

- li 안에는 버튼이 2개 있다. 삭제와 finished로 이동시키는 버튼.
- finished로 이동할 땐 다시 pending으로 보내는 버튼이 생긴다.

1. 우선 click "event"가 발생한 버튼의 지점을 찾아야한다. e.target을 사용한다.
2. 그리고 li가 넘어가면 클릭된 버튼의 text가 변경되어야 한다. (btn.innerText = '변경할 text');
3. li을 담고있는 ul의 id값을 if 조건에 넣어 ul의 id를 바꾸는 것을 통해 li의 위치와 버튼의 text를 바꾼다.

```javascript
if (id === "pending") {
  target = document.getElementById("finish");
  btn.innerText = "reset";
}
```

## 5. splice와 indexOf로 로컬스토리지 data 삭제하기 추가하기

1. splice()는 [배열명].splice([항목 위치], [삭제할 항목 수], [추가할 항목] ...); 으로 쓰인다. 배열의 항목을 컨트롤할 때 사용.

- e.target된 리스트를 삭제하려면 리스트를 찾아야 한다.

2. indexOf()는 특정 값을 찾아 삭제할 수 있다.

- string.indexOf(searchvalue, position)
- searchvalue : 필수 입력값, 찾을 문자열
- position : optional, 기본값은 0, string에서 searchvalue를 찾기 시작할 위치

3. indexOf에 들어간 value는 li의 id값이다. 전체범위(0)에서 li의 id값만 찾아 지우는 것이다.

```javascript
pendingData.splice();

//

pendingData.splice(pendingData.indexOf(value), 0);
```

4. splice + indexOf를 통해 pending에서 지운 후, finish 배열에 지운 값을 다시 넣는다.

```javascript
finishData.push({
  id: value,
  text: text,
});

saveData();
```

<img src="/images/posts/moveitem.png">

## 6. 로컬스토리지에 저장된 값을 새로고침 시 불러오기

1. 로컬스토리지에 저장된 값이 null일 때 (값이 있으면) 불러오게 설정한다.
2. JSON을 이용하여 저장한 것처럼 불러올 때도 JSON.parse으로 불러온다.
3. forEach 반복문을 통해 각 data의 text값을 paint함수로 실행한다.

![loadData](/images/posts/loadData.png)

---

## 후기

2일에 걸쳐 작업했고, 하루동안 작업한 결과물은 엎었다.

아무래도 강의 내용보다 과제가 난이오가 5는 더 올라간 느낌이라 그런지 input에는 submit이벤트가 안되는구나를 3시간 동안 끙끙대다 알게되었다.

유튜브와 구글에서 투두리스트를 만드는 것을 찾아보고, 섞어 사용하였다.

챌린지는 앞으로 5일 남았다. 비록 오늘 과제는 모든 기능을 구현하지 못했지만, 포기하지 않고 끝까지 했음에 나름 만족한다.
