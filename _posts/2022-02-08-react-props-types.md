---
layout: post

title: react - PropsTypes

tags: [React]

image:
---

### props 의 조건 정하기

- props에는 다양한 타입의 값이 전달될 수 있다. 하지만 만약에 다른 사람과 협업했을 경우, 내가 정한 string에 다른 사람이 number를 보내면 어떻게 될까? 놀랍게도 리액트 문법에는 틀린 것이 아니기 때문에 아무런 경고를 보내주지 않는다. 그렇다면 이러한 이슈를 보는 시점은 이미 서비스에 적용된 이후일 것이다. 사용자가 보기 전에 발견하면 다행이지만 ..
- 이러한 상황을 예방하기 위해 PropsType을 정할 수 있다.
- PropsType은 각기 다른 타입들을 검사할 수 있다.
- 문법은 아래와 같다.

```PropName.propTypes = {
  text:string,
  fontSize: number,
}
```

- 기본 문법을 예제에 적용을 해보자면

```javascript
// const Btn = ({ text, onClick. fontSize }) => {
//   return <button style={{fontSize}}onClick={onClick}>{text}</button>;
// };

Btn.propTypes = {
  text: string,
  fontSize: number,
};

// function PracSecond() {
//   const [value, setValue] = useState("확인");
//   const onClick = () => setValue("변경");

//   return (
//     <>
//       <div>
//         <memoBtn text={value} fontSize={18} onClick={onClick}></memoBtn>
//         <memoBtn text="취소"></memoBtn>
//       </div>
//     </>
//   );
// }
```

- Btn의 prop타입은 text : string, fontSize : number로 정의했다.
- 이제 콘솔에서 해당 타입과 맞지 않는 값을 전달할 경우 경고가 뜨게 될 것이다.
- 그런데 이 문법은 선택적이다. number가 들어가는것을 권고할 뿐 필수의 역할은 하지 않는다.
- 확실하게 number만 받고 싶다면 `.isRequired` 붙이자.

```javascript
Btn.propTypes = {
  text: string,
  fontSize: number.isRequired,
};
```

- 이렇게 하면 fontSize에는 무조건 숫자만 들어오게 작동하게 된다.
