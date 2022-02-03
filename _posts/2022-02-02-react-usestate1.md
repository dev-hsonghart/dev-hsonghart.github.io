---
layout: post

title: react - useState 01. input에 입력한 값 감지하고 함수 적용하기

tags: [React, Hook]

image:
---

### Input과 Onchange

- Input의 Onchange 속성에 useState의 함수를 활용하면 input안에서 이벤트(변화)가 발생할 때 해당 함수가 작동한다.
- input내 변화를 감지하는 변수명은 event 혹은 e 로 사용한다.

```javascript
import { useState } from "react";

function Prac() {
  // function
  const [data, setData] = useState();
  const onChange = (e) => setData(e.target.value);

  return (
    <>
      <label form="id">하나씩 더하기 : </label>
      <input
        id="id"
        onChange={onChange}
        // event 발생 시 onChange에 저장된 함수가 작동한다.
        placeholder="숫자만 입력"
        type="number"
      ></input>
      <h3>결과 : {parseInt(data) + 1}</h3>
    </>
  );
}

export default Prac;
```

<img src="/images/posts/react-prac-01.png">

- value : input에 입력된 값
- e.target.value : 이벤트가 발생된 곳의 input의 값
- onChange : input에서 이벤트(변화)가 발생할 때 입력한 함수가 작동하는 속성값

<br/>
즉, input에 입력이 감지가 되면 onChange에 등록된 함수가 작동하게 된다.
onChange 함수는 이벤트의 입력값을 data에 그대로 전달만 하게 된다.
이 전달된 data를 결과 란에서 수식이나 다른 함수를 만들어 변화를 주면 된다.
그리고 이 data는 string으로 전달되기 때문에, 사칙연산을 할 때 숫자로 바꿔야(parseInt(data)) 사칙연산이 적용된다.

### Tip

- styled-components를 함수 안에 작성할 경우 의도치않은 리렌더링이 발생한다.
- 함수 밖으로 빼내어 전역변수로 사용하도록 해야 계속 렌더링이 되는 현상이 일어나지 않는다.
