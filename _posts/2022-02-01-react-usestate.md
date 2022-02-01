---
layout: post

title: react - useState

tags: [React, Hook]

image:
---

### 리액트 훅 useState

useState 란 사용자와의 상호작용을 통해 바뀌는 값(DATA)의 상태를 관리하는 함수이다.
하드코딩을 하게 되면 값이 바뀔때마다 매번 렌더링을 해줘야하기 때문에, 이를 간편하게 하기 위해 Hook을 사용하는 것이다.

useState를 호출 시 다음과 같은 배열을 반환한다.

[DATA, function]

DATA 에는 바뀌는 값이고, function은 DATA를 변경해주고 돌려주는 함수이다.
예를 들자면, 쇼핑사이트에서 구매수량을 DATA / 구매수량을 조절하는 기능을 function으로 이해하면 된다.
그리고 useState()의 괄호 안에 들어가는 값은 DATA의 초기 값이다. 구매수량이 기본적으로 1개로 셋팅되어 있는 것처럼 말이다. 기본값에는 string, number, boolean 이 사용가능하다.

### useState 는 어떻게 쓰는가?

위에서 말했듯이 useState()는 "배열"을 반환한다.
DATA와 function을 쓰기 위해선 따로 꺼내어 주어야 한다.

```javascript
const DATAState = useState(0);
const DATA = useState[0];
const setDATA = useState[1];
```

이렇게 정의하고 사용해도 되지만 매번 3줄을 반복적으로 쓰는 것은 귀찮은 일이다.
배열을 좀 더 간단하게 지정하는 방법을 보도록 하자.

const [A,B] = object
이렇게 지정하면 A에는 object[0]/ B에는 object[1]이 순차적으로 정의된다.

```javascript
const [DATA, setDATA] = useState(0);
```

세줄이 한줄로 바뀌게 되면서 좀 더 섹시한 코드를 짤 수 있게 되었다.
그리고 function의 이름을 지을 땐 DATA이름 앞에 set을 붙이는 것으로 암묵적으로 약속되어 있다.
물론 하고싶은대로 해도 되지만, 협업을 할 경우엔 이와 같은 약속을 지켜주는 것이 유지보수 시에 좋다.

<br/>

이제 정의는 내렸으니, 값을 변경해보자.

DATA는 구매수량이고, 구매수량을 조절하는 함수를 만들어서 리턴해보자.
DATA의 값을 변경하는 함수는 setDATA(여기에 수식을 넣어주면 된다.)

```javascript

function App(){
  const [counter, setCounter] = useState(0);
  const counterUp = () => setCounter(counter + 1);
  const counterDown = ()=>setCounter(counter - 1);

  return (
    <h2>구매수량 : {counter}</h2>
    <button onClick={counterUp}> + </button>
    <button onClick={counterDown}> - </button>
  );

}
export default App;
```

setCounter()의 함수의 수식은 정의되지 않았고, 값을 변경해주고 반환해주기 때문에 변경되는 값이 동일하다면 하나의 함수로 수식만 바꾸어 더하고, 빼는 등으로 활용하면 된다.

button 태그에 함수를 붙이는 방법은 onClick={함수명}을 쓰면 된다.

이렇게 하면 구매버튼을 누를 때마다 구매 수량만 업데이트 되는 것을 확인할 수 있다.

<br/>

### 만약 값이 다른 곳에서도 바뀐다면?

내가 지정한 구매 수량이 이 화면 외 다른 화면에서도 조절이 된다면, counter에 정의한 useState의 기본값을 유지하게 되면 다른화면에서 변경된 값이 유지되지 않을 것이다.
그러면 현재값을 사용하면 된다.

```javascript

function App(){
  const [counter, setCounter] = useState(0);
  const counterUp = () => setCounter((currnet)=>current +1);
  const counterDown = ()=>setCounter((currnet)=>current -1);

  return (
    <h2>구매수량 : {counter}</h2>
    <button onClick={counterUp}> + </button>
    <button onClick={counterDown}> - </button>
  );

}
export default App;
```

setDATA()안에 current값을 리턴해주는 함수로 한번 더 감싸준다.
current는 현재 값을 불러오는 것으로 활용하도록 하자.

- 즉, 기존 값과는 다른 값으로 시작할 경우엔 DATA를 그대로 쓰면 되지만,
- 다른 화면에서 유지되어야할 값을 사용할 경우 current를 사용하도록 하자.
