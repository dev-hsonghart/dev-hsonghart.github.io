---
layout: post

title: 가상 선택자(::after, ::before)를 이용한 애니메이션 시 유의사항

tags: [css]

image:
---

### ::after와 ::before에 애니메이션 속도 설정할 때!

- 위의 가상 선택자에 기존 class와 다른 애니메이션을 설정할 때 재생속도가 기존 class와 같으면 가상 선택자의 애니메이션이 작동이 안되는 것을 발견할 수 있다.
- 이 경우는 기존 class와 다른 애니메이션을 적용할 때 나타난다.
- 즉 같은 애니메이션을 적용할 땐 재생속도가 같아도 작동이 된다.
- 이를 토대로 (정확한 이유는 모르겠지만) 내 생각에 기존 class의 애니메이션과 어떠한 충돌(?)을 일으켜서 작동을 안하는 것 같다.

---

작동하는 경우

```css
/* 적용 애니메이션과 재생 속도가 같을 경우 */
.__010 {
  animation: rotate 1s linear infinite;
}
.__010::after {
  animation: rotate 1s linear infinite;
}
```

```css
/* 적용 애니메이션과 재생 속도가 다를 경우 */
.__010 {
  animation: reverseRotate 1s linear infinite;
}
.__010::after {
  animation: rotate 0.5s linear infinite;
}
```

작동 안하는 경우

```css
.__010 {
  animation: reverseRotate 1s linear infinite;
  /* 기존 클래스만 작동한다. */
}
.__010::after {
  animation: rotate 1s linear infinite;
  /* 가상 클래스는 작동하지 않는다 */
}
```
