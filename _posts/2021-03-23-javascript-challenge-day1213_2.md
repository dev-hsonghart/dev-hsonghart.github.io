---
layout: post

title: js-api로 날씨 정보 불러오기 - 01

tags: [javascript, frontend, blog, api, 날씨 정보]

image:
---

### navigator 객체

- 브라우저에 대한 다양한 정보를 저장하는 객체 이다.

### geolocation

- 사용자의 위치 정보에 대한 navigator 속성이다.
- 사용자가 디바이스 설정에서 위치 정보에 대한 접근 권한을 허용한 경우메나 사용이 가능하다.

### getCurrentPosition(success() , error())

- 사용자의 현재 정보를 불러온다.
- 성공했을 때의 함수와 에러인 경우의 함수가 필수로 필요하다.

```javascript
function askForCoords() {
  navigator.geolocation.getCurrentPosition(handleGeoSuccess, handleGeoError);
}
```

- 현재 위치 중 위도와 경도를 저장한다.

```javascript
function handleGeoSuccess(position) {
  const latitude = position.coords.latitude,
    longitude = position.coords.longitude;
  const coordsObj = {
    latitude,
    longitude,
  };
  saveCoords(coordsObj);
}
```

> 객체에 저장을 할 때 key와 value를 갖게 하려면 한번만 사용하면 된다.

- 위치를 불러올 수 없을 경우도 설정해 준다.

```javascript
function handleGeoError() {
  console.log("위치에 접근할 수 없습니다.");
}
```

이렇게 불러온 경도와 위도를 이용하여 날씨 정보를 불러오자.
