---
layout: post

title: react - props

tags: [React]

image:
---

### 컴포넌트에 value를 전달하고싶다면?

<img src="/images/posts/react-props-01.png">

- 같은 스타일의 버튼인데, 버튼명이 다를 경우에 props을 사용할 수 있다. 이미 생성된 컴포넌트에 특정 인자값을 전달할 수 있는 것이다.

```javascript
const Btn = (props) => {
  return (
    <button style={{ backgroundColor: "tomato", color: "white" }}>
      {props.text}
    </button>
  );
};

function PracSecond() {
  return (
    <>
      <div>
        <Btn text="확인"></Btn>
        <Btn text="취소"></Btn>
      </div>
    </>
  );
}
```

- Btn에 `text="확인" ` 이 부분이 props에 해당된다. 리액트는 이 부분을 읽어 props이라는 object로 컴포넌트에 전달해준다.
- object이기 때문에 text를 컴포넌트에서 사용할 땐 props.text, 즉 props의 text를 써달라고 풀어서 전달해야한다.
- 이것보다 좀 더 간단한 방법은 array의 요소를 순차적으로 지정하는 방식을 활용하자.

```javascript
const Btn = ({ text }) => {
  return (
    <button style={{ backgroundColor: "tomato", color: "white" }}>
      {text}
    </button>
  );
};

function PracSecond() {
  return (
    <>
      <div>
        <Btn text="확인"></Btn>
        <Btn text="취소"></Btn>
      </div>
    </>
  );
}
```

- array를 꺼내어 정의할 때는 [a, b]를 쓴 것처럼 object에서는 {a,b}로 사용하면 된다. 물론, 정의는 이미 내려졌기 때문에 props key를 그대로 사용하면 된다.
- `props.text => {text}`
- 이러면 좀 더 간결하고 짧은 코드를 사용할 수 있다.

<br/>

- props에는 string말고도 숫자, boolean, 함수까지 전달할 수 있다.

### props. 기본값 설정

- 버튼 스타일은 같으나 색상이나 size 등이 조금씩 다른 ui도 있을 수 있다. 이럴 경우엔 기본적인 ui를 정하고 변경되는 부분만 전달해주면 된다.
- props. 의 기본값을 정할 때는 아주 간단하다.
- 컴포넌트에 전달할 때 key = 기본값 으로 써주면 된다.

```javascript
const Btn = ({ text, fontSize = 14 }) => {
  return (
    <button style={{ fontSize, backgroundColor: "tomato", color: "white" }}>
      {text}
    </button>
  );
};

function PracSecond() {
  return (
    <>
      <div>
        <Btn text="확인" fontSize={20}></Btn>
        <Btn text="취소"></Btn>
      </div>
    </>
  );
}
```

<img src="/images/posts/react-props-02.png">

- 확인 버튼은 20px/ 취소는 폰트사이즈의 기본값인 14px로 적용된다.
- 그리고 props key 이름과 css key 이름이 동일한 경우 하나만 적자. 알아서 적용된다.

### props는 props일 뿐이다.

- props는 이벤트 리스너가 아니다. props가 전달해주는 것은 정말 단순한 value일 뿐이다.
- 예를 들어, button의 onClick에 넣고 싶어서 props이름을 onClick으로 작성해도 이것은 단순 onClick이라는 이름의 데이터값에 지나지 않는다.
- 그렇기 떄문에 컴포넌트 안에서 해당 onClick 값을 직접 달아주어야 작동하게 된다.

```javascript
const Btn = ({ text }) => {
  return <button>{text}</button>;
};

function PracSecond() {
  function onClick() {
    return "변경";
  }
  return (
    <>
      <div>
        <Btn text="확인" onClick={onClick}></Btn>
        <Btn text="취소"></Btn>
      </div>
    </>
  );
}
```

- onClick이라는 함수를 생성하여 onClick이라는 이름으로 props에 넣은 것뿐, <button>태그에 직접 달아주는 게 아닌 이상 작동하지 않는다.

```javascript
const Btn = ({ text, onClick }) => {
  return <button onClick={onClick}>{text}</button>;
};

function PracSecond() {
  const [value, setValue] = useState("확인");
  const onClick = () => setValue("변경");

  return (
    <>
      <div>
        <Btn text={value} onClick={onClick}></Btn>
        <Btn text="취소"></Btn>
      </div>
    </>
  );
}
```

<img src="/images/posts/react-props-03.png">

<br/>

### 불필요한 리렌더링이 일어난다면?

- 자식요소에서 useState를 이용하여 상태값이 변경될 때마다 부모 함수는 전체적으로 랜더링을 또 하게 된다.
- ui요소가 적을 땐 큰 이슈는 아니지만, 서비스 안에서는 컴포넌트 요소가 한두개가 아닐 것이다. 이럴 경우에 리렌더링이 반복적으로 일어난다면 문제가 될 것이다.
- 이를 해결해주는 것이 memo(컴포넌트) hook이다.
- memo는 memorize(기억하다)로, props이 변경되지 않는 ui는 리렌더링을 할 필요가 없다는 것을 리액트에게 알려주는 것이다.

```javascript
const Btn = ({ text, onClick }) => {
  console.log(`${text} 바뀜`);
  return <button onClick={onClick}>{text}</button>;
};

const memoBtn = memo(Btn);

function PracSecond() {
  const [value, setValue] = useState("확인");
  const onClick = () => setValue("변경");

  return (
    <>
      <div>
        <memoBtn text={value} onClick={onClick}></memoBtn>
        <memoBtn text="취소"></memoBtn>
      </div>
    </>
  );
}
```

<img src="/images/posts/react-props-04.png">

- `const memoBtn = memo(Btn)` 이 코드를 통해 취소 버튼은 리렌더링이 일어나지 않는 것을 콘솔창에서 확인할 수 있다.
- 만약 너무 많은 리렌더링이 일어나 서비스 속도가 느려졌다면 불필요하게 렌더링이 일어나는 부분을 체크해보자.
