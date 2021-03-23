---
layout: post

title: api로 날씨 정보 불러오기 - 02

tags: [javascript, frontend, blog, api, 날씨 정보]

image:
---

### API

- api는 일종에 키보드라고 이해하면 된다. 타자를 입력하면 출력되는 것처럼 원하는 데이터를 입력(request)하여 출력(reponse)받는다.

### openweathermap API

- openweathermap : https://openweathermap.org/api

- 해당 사이트에 가입을 하면 API-key를 발급받을 수 있다.

### fecth()

- 첫번째 인자로 URL, 두번째 인자로 옵션 객체를 받고, Promise 타입의 객체를 반환합니다.
- 반환된 객체는, API 호출이 성공했을 경우에는 응답(response) JSON 객체를 resolve하고, 실패했을 경우에는 예외(error) 객체를 reject한다.

```javascript
function getWeather(lat, log) {
  fetch(
    `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=${API_KEY}&units=metric`
  );
}
```

### then

- 이전 자바스크립트 코드가 완전히 실행돼서 데이터가 넘어왔을 때만 실행되게 하는 함수이다.

```javascript
fetch(
  `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=${API_KEY}&units=metric`
).then(function (response) {
  return response.json();
});
```

### 도시이름, 날씨, 온도의 상수를 설정하자.

- reponse된 JSON 객체를 console.dir해보자. 객체 정보를 읽어볼 수 있다.
- 온도는 소수점을 가지고 있으므로 소수점을 버리고 싶다면 Math.floor 를 활용하자.

```javascript
const currentCity = json.name,
  currentTemp = Math.floor(json.main.temp),
  currentWeather = json.weather[0].main;
```

- innerText 를 이용하여 html에 JSON 데이터를 출력하자.

```javascript
cityDisplay.innerText = currentCity;
tempDisplay.innerText = `${currentTemp} ˚`;

if (currentWeather === "Clouds") {
  //날씨가 흐릴 때
  skyDisplay.innerText = "☁️";
} else if (currentWeather === "Thunderstorm") {
  //날씨가 천둥번개일 때
  skyDisplay.innerText = "⛈";
} else if (currentWeather === "Drizzle") {
  //날씨가 부슬비 때
  skyDisplay.innerText = "🌦";
} else if (currentWeather === "Rain") {
  //날씨가 비 내릴 때
  skyDisplay.innerText = "🌧";
} else if (currentWeather === "Snow") {
  // 날씨가 눈 내릴 때
  skyDisplay.innerText = "❄️";
} else if (currentWeather === "Clear") {
  //날씨가 화창할 때
  skyDisplay.innerText = "☀️";
}
```
