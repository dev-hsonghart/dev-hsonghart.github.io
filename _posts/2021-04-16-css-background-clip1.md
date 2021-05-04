---
layout: post

title: background clip을 이용해서 border에 gradient 효과 주기

tags: [css]

image:
---

<br>
### border radius 와 border gradient는 같이 사용될 수 없다!

- 다양한 loader를 만들던 중, 원형 border에 gradient가 적용되지 않았다.
- 원형은 사각형에 border-radius를 50%로 설정하여 만들었는데, 찾아보니 border-radius 와 사용할 수 없다는 것이다.

### background clip ?

- background clip은 배경 이미지나 배경 색을 어느 범위까지 채울 지 설정할 수 있다.
- border-box : 테두리 영역 부터 그 안쪽 영역.
- padding-box : 안쪽 여백 영역(테두리 영역을 제외)부터 그 안쪽 영역.
- content-box : 내용 영역과 그 안쪽 영역.
- initial : 기본값.
- inherit : 부모 요소의 속성값을 상속.

### border-box 와 padding-box를 이용해 border에 gradient가 된 것처럼 보이게끔!

1.border-radius와 border를 설정하자. 왜냐하면 border-box 속성도 사용해야 하기 때문이다.

```css
.circle {
  border-radius: 50%;
  border: solid 3px transparent;
}
```

2.이제 background에 컬러를 채우면 된다. border-box에 원하는 그라디언트 색상을 채우자.

<img src="/images/posts/border-gradient-01.png">

```css
.circle {
  border-radius: 50%;
  border: solid 3px transparent;
  background: linear-gradient(to right, var(--main-clr), var(--main-clr-800)) border-box;
}
```

3.그라디언트 컬러 뒤에 clip 속성을 넣게 되면 clip 설정에 맞게 채워지게 된다. 이제 border를 제외한 영역(padding-box)에 배경색을 설정하게 되면.
<img src="/images/posts/border-gradient-02.png">

```css
.circle {
  border-radius: 50%;
  border: solid 3px transparent;
  background: linear-gradient(#000, #000) padding-box, linear-gradient(
        to right,
        var(--main-clr),
        var(--main-clr-800)
      ) border-box;
}
```

4.border 라인에 그라디언트가 적용된 것처럼 보인다.

---

디자인 할 때처럼 쉽게 만들 수 있던 게 css에서는 안될 때가 있다. <br> 그럴 때는 포토샵을 썼던 때를 떠올려서 정말 1차원적으로 접근하면 해결이 가능한 듯 하다. <br> 물론 난 구글링을 했지만.. 구글링 최고!
