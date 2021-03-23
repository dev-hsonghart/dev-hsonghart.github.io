---
layout: post

title: 로컬 스토리지에 데이터 저장하기

tags: [javascript, frontend, blog]

image:
---

자바스크립트 챌린지 day6.
벨로그에서 옮기는 중

---

### Local Storage

- 작은 단위 정보를 유저 컴퓨터에 저장하는 방법
- localStorage.setItem("key", "value")
- localStorage.getItem("key", "value")
- set은 setting하므로 저장
- get은 가져오므로 불러오기 라고 이해하면 편하다
- 로컬스토리지에 저장할 때 데이터 타임을 "string"을 기본타입으로 저장한다.

### selectedIndex

- select 태그의 선택값을 반환해준다.
- select + option 은 드롭다운 박스인데, 이 안에는 최소 2개부터 선택 항목이 다양하기에 option을 js에서 불러올 때 array가 된다.
- 즉, 유저가 선택한 option을 저장하려면 선택한 option을 값으로 변환해야하고, selectedIndex가 이 기능을 수행한다.

```javascript
const selectForm = document.querySelector("select");
// html의 select태그 선언

function saveSelectData(value){
localStrage.setItem("Data", value);
}
// 로컬스토리지에 특정 값을 저장하는 함수 정의

function saveSelect(){
const selectedData = selectForm.value;
// select에서 선택한 Index값을 선언

const selectIndex = selectForm.selectedIndex;
// 이 상수가 없어도 로컬리지에 저장이 되나 0번째 항목도 저장되기 때문에 if에 쓰기 위해 선언

if(selectIndex > 0){
	saveSelectData(selectedData);
	}
// select에서 0번째 항목은 placeholder의 기능이므로 0을 제외한 항목을 선택할 경우 값을 저장하도록 설정.

saveSelect(); // 실행
```
