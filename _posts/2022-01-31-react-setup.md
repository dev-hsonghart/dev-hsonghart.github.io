---
layout: post

title: react - 셋팅

tags: [React]

image:
---

### 리액트를 처음 설치한다면!

os의 터미널 창을 열어서 설치하고자 하는 폴더로 이동한다.
터미널에서 경로를 이동하는 명령어는 `cd ~~` 이다.
그리고 설치하고자 하는 폴더 위치는 폴더 주소를 우클릭하면 복사할 수 있다.
그 후 설치 명령어를 쓴다.

```
cd "이동할 폴더 경로"
npx create-react-app "프로젝트 이름"
```

<br/>

### 스타일 컴포넌트를 설치하자!

설치가 완료되었다면 생성한 프로젝트 폴더 안으로 이동하자.
이동하지 않은 채로 style-component 설치를 시도할 시 설치 실패를 하게 된다.

```
cd "생성한 프로젝트 이름"
npm i styled-components
```

<br/>

### css reset을 설치하자!

매번 어느 블로그, 깃헙, 따로 복사한 코드 등을 복붙하기는 슬슬 귀찮아진다.
터미널을 통해 다운받아서 활용해보자.

```
npm istall styled-reset
```

<br/>

그리고 global로 적용하는 css를 만들기 위해 'createGlobalStyle'을 styled-components로부터 import 해줘야 한다. 방금 설치한 styled-reset도 같이 import하자.

```javascript
import { createGlobalStyle } from "styled-components";
import reset from "styled-reset";
```

<br/>

그리고 GlobalStyles 라는 컴포넌트를 생성하자.

```javascript
const GlobalStyles = createGlobalStyle`
${reset}`
// 추가로 변경하고 싶은 사항을 작성
* {
    box-sizing: border-box;
  }
;

export default GlobalStyles;
```

"reset" 다음으로 폰트를 바꾸거나, 추가적으로 수정하고자 하는 사항이 있으면 적도록 하자.
이제 생성한 GlobalStyles를 app에 작성하면 css가 reset된다.

### propTypes 도 추가로 설치하자.

- 리액트의 prop을 다룰 때 타입들을 체크해주는 아주 유용한 기능이다.

```javascript
npm i prop-Types

import PropTypes from "prop-types";
```

### 이렇게 셋팅하면 초기 환경이 완성되었다!
