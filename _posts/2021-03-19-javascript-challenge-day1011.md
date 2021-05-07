---
layout: post

title: js-계산기 만들며 익힌 함수

tags: [javascript, frontend, blog, 계산기]

image:
---

챌린지 일지 Day10~11. 2021 03 19

---

### 계산기 만들기

- 기본 구현 기능

1. 기본적인 사칙연산
2. 등부호(=)를 통해서만 연산 실행
3. 리셋 기능
4. 2를 연속으로 곱할 경우 등부호 없이 연산 실행

---

## 1. selectorAll로 불러온 객체"들"에 event 달기

> 사용한 함수 : for 반복문

- 계산기에는 0부터 9의 숫자 버튼과 사칙연산 버튼이 있다. 이 둘의 공통점은 버튼 텍스트만 다를 뿐, 기능은 같다는 것이다. 연산은 연산 기능, 숫자는 해당 숫자를 디스플레이에 입력하는 것.
- selectorAll로 불러온 버튼들은 배열로 묶어 **btnNum** 에 저장한다.
- 배열 안 객체마다 함수를 **반복** 실행하기 위해 **for** 반복문을 사용한다.

### 1-1. for 반복문

```javascript
배열.for(초기화; 반복문 실행 조건; 반복 후 처리){
  함수
}
```

- btnNum를 하나씩 불러와 차례대로 이벤트를 달 수 있다.
- for의 조건에는 btnNum 안 객체들을 순서대로 불러오게 설정한다.
- 그 다음 실행 내용을 통해 이벤트를 달아 놓는다.

```javascript
for (let i = 0; i < btnNum.length; i++) {
  btnNum[i].addEventListener("click", displayValue);
}
```

- i에 0을 저장하여 초기화를 한다.
- btn.Num의 길이가 0보다 크면 {btn.Num의 i번째(처음은 0번째)에 이벤트를 적용한다.}
- 그리고 i에 1을 더한다.

이 반복문은 i가 btn.Num의 길이, 즉 배열 안 객체 갯수보다 i가 더 클 때 멈추게 된다.
그래서 i는 상수가 아닌 변수로 저장해야 한다.

---

## 2. eval();

- 버튼들을 불러와 이벤트를 달아주었다.
- 이벤트는 버튼의 "텍스트"를 calcText 영역에 뿌려주게 설정하였다.
- 연산은 숫자를 계산하고 "텍스트"는 연산이 실행되지 않는다.
- eval()를 이용하면 텍스트를 강제 실행시키게 되는데, 그러면 숫자가 아니어도 연산이 가능하게 된다.

```javascript
displayResult.innerText = eval(calcText);
```

### eval = evil

- 구글링을 하다보면 eval은 쓰면 안된다고 한다.
- 이유는 보안 위험과 eval의 수행 능력이 좋은 편이 아니기 때문에 eval은 **절대** 써선 안된다.
  (계산기를 다시 만들 땐 지금과 다른 방법으로 만들어 봐야 겠다.)

---

## 3. clssName 을 체크하여 함수 분기 처리

- 연산 실행까지 작동한다면, 이제 특정 예외에 대한 처리를 생각하게 된다.
  - 연산자가 연속 입력되면 안된다.
  - 연산자가 마지막 입력일 경우 등부호가 작동하지 않아야 한다.
  - 빈 화면에 연산자가 입력되면 안된다.
  - 화면에 0만 있고 + 숫자가 입력될 경우 => 0을 지우고 숫자만 표시해야 한다.
  - 등등..

### 3-1. 연산자, 숫자, 등부호 등 버튼 실행 시 각각 설정한 class가 특정 html element에 추가하게 한다.

```javascript
const calcText = document.querySelector("span");

function addCalc(event) {
  const targetCalc = event.target.innerText;
  calcText.innerText = calcText + `${targetCalc}`;
  calcText.classList.add("addCalc");
}
```

- 위 함수는 사칙연산 이벤트 리스너에 붙은 함수인데, 타겟의 텍스트를 calcText로 보내고 calcText에 "addCalc" 클래스를 붙였다.
- **클래스를 넣고 싶을때 classList.add("넣을 클래스")를 사용한다.**
- 반대로 삭제하고 싶을 땐 **ad**d를 **remove**로 바꾸면 된다.
- "addCalc"이 붙여있을 경우 이미 연산자를 입력했다는 뜻으로 사용하였다.
- 연산자가 연속 입력이 되면 안되기 때문에 calcText에 "addCalc"이 없을 경우만 실행하라는 if조건문을 달았다.

### 3-2. classList

- 위 조건을 달고 싶으면 calcText의 class에 "addCalc"이 있는지 알아야 한다.
- classList.contains(검색대상) 를 통해 체크가 가능하다.
- 검색대상이 있으면 true를, 없으면 false를 반환한다. 이제 조건문을 달아보자.

```javascript
const calcText = document.querySelector("span");

function addCalc(event)
  if(calcText.classList.contains("addCalc") !== true) {
    const targetCalc = event.target.innerText;
    calcText.innerText = calcText + `${targetCalc}`;
    calcText.classList.add("addCalc");
}
```

- 이런 식으로 다른 예외처리를 추가하였다.

---

## 4. indexOf()

```javascript
대상문자열.indexOf(검색대상, [시작위치]);
```

- 특정 문자열을 검색하는 함수
- 검색대상이 있을 경우 , 해당 위치를 반환한다.
- 없을 경우 -1을 반환한다.

### 4-1. 계산기 기능 중 2를 연속 곱할 경우 등부호없이 바로 연산되어야 한다.

- 관련된 식을 쓰면 2x2x2x2x...가 된다.
- 위 조건은 2번째 곱셈부터 분기를 정하여 처리해야한다.
- 2번째 곱셈 이전 문자는 2x2이다.
- 그러므로 2x2가 있으면 무조건 연산처리를 진행하게 한다.

```javascript
if (calcText.indexOf("2*2") === 0) {
  // 2를 연속으로 곱할 경우 등부호 없이 바로 결과 출력
  calcHidden.innerText = calcText + `${targetCalc}`;
  displayResult.innerText = eval(calcText);
  hiddenClass.add("timeTwo", "addCalc");
}
```

- 이제 문자열에 "2x2"가 있는지 확인해야 한다.
- indexOf를 이용해 "2x2"가 맨 앞에 있는지 체크하고 있을 경우에 실행되게 한다.

### 4-2. 2x2x5일 경우는?

- 조건을 하나 넣었지만, 위와 같은 수식일 경우에도 작동한다는 이슈가 생겼다.
- 문자열에 2와 \*만 있을 경우에만 작동하게 해야 할까?
  - 이 조건을 넣을 수 있는 함수를 모르겠다..
- 그러면 2가 홀수자리, \*이 짝수자리일 때 작동하게 할까?
  - 짝수, 홀수를 구하는 함수를 만들었지만 if문 안에서 작동하지 않았다...
- indexOf 검색 대상에 2와 \*을 제외하고 다 넣어 검색하게 해볼까?
  - indexOf는 단일만 검색이 된다....

```javascript
if (
  calcText.indexOf("2*2") === 0 &&
  hiddenText.indexOf("1") === -1 &&
  hiddenText.indexOf("3") === -1 &&
  hiddenText.indexOf("4") === -1 &&
  hiddenText.indexOf("5") === -1 &&
  hiddenText.indexOf("6") === -1 &&
  hiddenText.indexOf("7") === -1 &&
  hiddenText.indexOf("8") === -1 &&
  hiddenText.indexOf("9") === -1 &&
  hiddenText.indexOf("0") === -1 &&
  hiddenText.indexOf("+") === -1 &&
  hiddenText.indexOf("-") === -1 &&
  hiddenText.indexOf("/") === -1
) {
  // 2를 연속으로 곱할 경우 등부호 없이 바로 결과 출력
  calcHidden.innerText = calcText + `${targetCalc}`;
  displayResult.innerText = eval(calcText);
  hiddenClass.add("timeTwo", "addCalc");
}
```

그냥 무식하게 &&로 묶어 2와 \*을 제외하여 다 집어넣었다.
... 😱
이렇게 자바스크립트로 만든 첫 계산기가 나왔다.

[계산기 링크](https://dev-hsonghart.github.io/first_calcurator/)
