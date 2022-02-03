---
layout: post

title: react - useState 02. state에 boolean을 이용하여 토글버튼 만들기

tags: [React, Hook]

image:
---

### useState()를 이용해서 토글 버튼을 만들자.

- useState의 data에는 string, number, "boolean"을 넣을 수 있다. 즉, on/off 상태를 다뤄볼 수 있다는 것이다.
- 앞서 만든 input을 활성, 비활성하는 기능을 만들어 보자.

<img src="/images/posts/react-prac-02.png">

```javascript
<label form="id">하나씩 더하기 : </label>
  <input
    id="id"
    onChange={onChange}
    placeholder="숫자만 입력"
    type="number"
    disabled={switched}
  ></input>
  <h3>결과 : {parseInt(data) + 1}</h3>
<button onClick={onDisabled}>{switched ? "활성화" : "비활성화"}</button>
```

<br/>

- input의 disabled 속성에 true일 때는 입력칸이 비활성 처리 된다. 이 상태를 이용해서 토글을 만들면 된다.

```javascript
const [switched, setSwitched] = useState(false);
const onDisabled = () => setSwitched((current) => (current = !current));
```

- 새로운 useState 함수를 사용하여 switched라는 데이터와 그에 맞는 함수를 정의한다.
- 기본적으로 입력칸은 활성화로 시작하기 때문에 false를 초기값으로 내린다.
- true <-> false 의 상태를 스위칭하기 위해서 현재 상태를 반대로 바꾸는 함수를 만들어 onDisabled에 저장한다.

```javascript
<button onClick={onDisabled}>비활성하기</button>
```

- button 의 onClick 속성에 위에 만든 onDisabled 함수를 넣으면 클릭 이벤트에 작동하게 된다.

<img src="/images/posts/react-prac-03.png">

```javascript
<button onClick={onDisabled}>{switched ? "활성화" : "비활성화"}</button>
```

- 마무리로 disabled 상태에 따라 텍스트가 다르게 나오게 만들어 사용성도 챙기자.
