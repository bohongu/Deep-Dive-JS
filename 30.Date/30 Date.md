# 30. Date

표준 빌트인 객체인 Date는 날짜와 시간(연, 월, 일, 시, 분, 초, 밀리초)을 위한 메서드를 제골ㅇ하는 빌트인 객체이면서 생성자 함수다.

## 30.1 Date 생성자 함수

Date 생성자 함수로 생성한 Date 객체는 기본적으로 현재 날짜와 시간을 나타내는 정수값을 가진다.

### 30.1.1 new Date()

Date 생성자 함수를 인수 없이 new 연산자와 함께 호출하면 현재 날짜와 시간을 가지는 Date 객체를 반환한다.

```jsx
console.log(new Date()); // 2023-09-27T09:51:15.842Z
```

Date 생성자 함수를 new 연산자 없이 호출하면 Date 객체를 반환하지 않고 날짜와 시간 정보를 나타내는 문자열을 반환한다.

```jsx
console.log(Date()); // Wed Sep 27 2023 18:51:34 GMT+0900 (대한민국 표준시)
```

### 30.1.2 new Date(milliseconds)

Date 생성자 함수에 숫자 타입의 밀리초를 인수로 전달하면 1970년 1일 1일 00:00:00:(UTC)을 기점으로 인수로 전달된 밀리초만큼 경과한 날짜와 시간을 나타내는 Date객체를 반환한다.

```jsx
// 한국 표준시 KST는 협정 세계시 UTC에 9시간을 더한 시간이다.
console.log(new Date(0)); // 1970-01-01T00:00:00.000Z

/*
86400000ms는 1day를 의미한다.
1s = 1,000ms
*/

console.log(new Date(86400000)); // 1970-01-02T00:00:00.000Z
```

### 30.1.3 new Date(dateString)

Date 생성자 함수에 날짜와 시간을 나타내는 문자열을 인수로 전달하면 지정된 날짜와 시간을 나타내는 Date객체를 반환한다.

```jsx
console.log(new Date("Sep 27, 2023 10:00:00")); // 2023-09-27T01:00:00.000Z

console.log(new Date("2023/09/27/10:00:00")); // 2023-09-27T01:00:00.000Z
```

### 30.1.4 new Date(year, month[, day, hour, minute, second, millisecond)

Date 생성자 함수에 연, 월, 일, 시, 분, 초, 밀리초를 의미하는 숫자를 인수로 전달하면 지정된 날짜와 시간을 나타내는 Date 객체를 반환한다. 연, 월은 필수값이다.

<p align='center'>
<img src='https://github.com/bohongu/Deep-Dive-JS/assets/91203029/8d0cdf25-94d7-4e18-8a33-4ebac451b3a8' />
</p>

```jsx
console.log(new Date(2023, 2)); // 2023-02-28T15:00:00.000Z

console.log(new Date(2023, 2, 28, 0, 0, 0, 0)); // 2023-03-27T15:00:00.000Z
```

## 30.2 Date 메서드

### 30.2.1 Date.now

1970년 1월 1일 00:00:00(UTC)을 기점으로 현재 시간까지 경과한 밀리초를 숫자로 반환한다.

```jsx
console.log(Date.now()); // 1695809135504
```

### 30.2.2 Date.parse

1970년 1월 1일 00:00:00(UTC)을 기점으로 인수로 전달된 지정 시간까지 밀리초를 숫자로 반환한다.

```jsx
// UTC
console.log(Date.parse("Jan 2, 1970 00:00:00 UTC")); // 86400000

// KST
console.log(Date.parse("Jan 2, 1970 09:00:00")); // 86400000
```

### 30.2.3 Date.UTC

1970년 1월 1일 00:00:00(UTC)을 기점으로 인수로 전달된 지정 시간까지의 밀리초를 숫자로 반환한다.

```jsx
console.log(Date.UTC(1970, 0, 2)); // 86400000
```

### 30.2.4 Date.prototype.getFullYear

Date 객체의 연도를 나타내는 정수를 반환한다.

```jsx
console.log(new Date("2023/09/27").getFullYear()); // 2023
```

### 30.2.5 Date.prototype.setFullYear

Date 객체에 연도를 나타내는 정수를 설정한다. 연도 이외에 옵션으로 월, 일도 설정할 수 있다.

```jsx
const today = new Date();

// 년도 지정
today.setFullYear(2023);
today.getFullYear(); // 2023
```

### 30.2.6 Date.prototype.getMonth

Date 객체의 월을 나타내는 0 ~ 11의 정수를 반환한다. 1월은 0, 12월은 11이다.

```jsx
console.log(new Date("2023/09/27").getMonth()); // 8
```

### 30.2.7 Date.prototype.setMonth

Date 객체에 월을 나타내는 0 ~ 11의 정수를 설정한다. 1월은 0, 12월은 11이다. 월 이외에 옵션으로 일도 설정할 수 있다.

```jsx
const today = new Date();

// 월 지정
today.setMonth(0); // 1월
today.getMonth(); // 0
```

### 30.2.8 Date.prototype.getDate

Date 객체의 날짜(1 ~ 31)를 나타내는 정수를 반환한다.

```jsx
console.log(new Date("2023/09/27").getDate()); // 27
```

### 30.2.9 Date.prototype.setDate

Date 객체에 날짜(1 ~ 31)를 나타내는 정수를 설정한다.

```jsx
const today = new Date();

// 날짜 지정
today.setDate(1);
today.getDate(); // 1
```

### 30.2.10 Date.prototype.getDay

Date 객체의 요일(0 ~ 6)을 나타내는 정수를 반환한다. 반환값은 다음과 같다.

<p align='center'>
<img src='https://github.com/bohongu/Deep-Dive-JS/assets/91203029/df0aadfd-fa94-48e2-97d1-25fc86cccdb3' />
</p>

```jsx
console.log(new Date("2023/09/27").getDay()); // 3
```

### 30.2.11 Date.prototype.getHours

Date 객체의 시간(0 ~ 23)을 나타내는 정수를 반환한다.

```jsx
console.log(new Date("2023/09/27").getDay()); *// 3*
```

### 30.2.12 Date.prototype.setHours

Date 객체에 시간(0 ~ 23)을 나타내는 정수를 설정한다. 시간 이외에 옵션으로 분, 초, 밀리초도 실정할 수 있다.

```jsx
const today = new Date();

// 시간 지정
today.setHours(7);
today.getHours(); // 7
```

### 30.2.13 Date.prototype.getMinutes

Date 객체의 분(0 ~ 59)을 나타내는 정수를 반환한다.

```jsx
console.log(new Date("2023/09/27/12:30").getMinutes()); // 30
```

### 30.2.14 Date.prototype.setMinutes

Date 객체의 분(0 ~ 59)을 나타내는 정수를 설정한다. 분 이외에 옵션으로 초, 밀리초도 설정할 수 있다.

```jsx
const today = new Date();

// 분 지정
today.setMinutes(50);
today.getMinutes(); // 50
```

### 30.2.15 Date.prototype.getSeconds

Date 객체의 초(0 ~ 59)를 나타내는 정수를 반환한다.

```jsx
console.log(new Date("2023/09/27/12:30:10").getSeconds()); // 10
```

### 30.2.16 Date.prototype.setSeconds

Date 객체의 초(0 ~ 59)를 나타내는 정수를 설정한다. 초 이외에 옵션으로 밀리초도 설정할 수 있다.

```jsx
const today = new Date();

// 초 지정
today.setSeconds(30);
today.getSeconds(); // 30
```

### 30.2.17 Date.prototype.getMillseconds

Date 객체의 밀리초(0 ~ 999)를 나타내는 정수를 반환한다.

```jsx
console.log(new Date("2023/09/27/12:30:10:150").getMilliseconds()); // 150
```

### 30.2.18 Date.prototype.setMillseconds

Date 객체의 밀리초(0 ~ 999)를 나타내는 정수를 설정한다.

```jsx
const today = new Date();

// 밀리초 지정
today.setMilliseconds(120);
today.getMilliseconds(); // 120
```

### 30.2.19 Date.prototype.getTime

1970년 1월 1일 00:00:00(UTC)를 기점으로 Date 객체의 시간까지 경과된 밀리초를 반환한다.

```jsx
onsole.log(new Date("2023/09/27/12:30").getTime());
1695785400000;
```

### 30.2.20 Date.prototype.setTime

Date 객체에 1970년 1월 1일 00:00:00(UTC)를 기점으로 경과된 밀리처를 설정한다.

```jsx
const today = new Date();

// 1970년 1월 1일 00:00:00(UTC)를 기점으로 경과된 밀리초 섲렁
today.setTime(86400000); // 86400000은 1day를 나타낸다.
console.log(today); // 1970-01-02T00:00:00.000Z
```

### 30.2.21 Date.prototype.getTimezoneOffset

UTC와 Date 객체에 지정된 로캘 시간과의 차이를 분 단위로 반환한다. KST는 UTC에 9시간을 더한 시간이다. 즉, UTC = KST - 9h다.

```jsx
const today = new Date();

// UTC와 today의 지정 로캘 KST와의 차이는 -9시간이다.
today.getTimezoneOffset() / 60; // -9
```

### 30.2.22 Date.prototype.toDateString

사람이 읽을 수 있는 형식의 문자열로 Date 객체의 날짜를 반환한다.

```jsx
const today = new Date("2023/9/27/12:30");

console.log(today.toString()); // Wed Sep 27 2023 12:30:00 GMT+0900 (대한민국 표준시)
console.log(today.toDateString()); // Wed Sep 27 2023
```

### 30.2.23 Date.prototype.toTimeString

사람이 읽을 수 있는 형식으로 Date 객체의 시간을 표현한 문자열을 반환한다.

```jsx
const today = new Date("2023/9/27/12:30");

console.log(today.toString()); // Wed Sep 27 2023 12:30:00 GMT+0900 (GMT+09:00)
console.log(today.toTimeString()); // 12:30:00 GMT+0900 (GMT+09:00)
```

### 30.2.24 Date.prototype.toISOString

ISO 8601 형식으로 Date 객체의 날짜와 시간을 표현한 문자열을 반환한다.

```jsx
const today = new Date("2023/9/27/12:30");

console.log(today.toString()); // Wed Sep 27 2023 12:30:00 GMT+0900 (GMT+09:00)
console.log(today.toISOString()); // 2023-09-27T03:30:00.000Z

console.log(today.toISOString().slice(0, 10)); // 2023-09-27
console.log(today.toISOString().slice(0, 10).replace(/-/g, "")); // 20230927
```

### 30.2.25 Date.prototype.toLocaleString

인수로 전달한 로캘을 기준으로 Date 객체의 날짜와 시간을 표현한 문자열을 반환한다. 인수를 생략한 경우 브라우저가 동작 중인 시스템의 로캘을 적용한다.

```jsx
const today = new Date("2023/9/27/12:30");

console.log(today.toString()); // Wed Sep 27 2023 12:30:00 GMT+0900 (GMT+09:00)
console.log(today.toLocaleString()); // 2023. 9. 27. 오후 12:30:00
console.log(today.toLocaleString("ko-KR")); // 2023. 9. 27. 오후 12:30:00
console.log(today.toLocaleString("en-US")); // 9/27/2023, 12:30:00 PM
console.log(today.toLocaleString("ja-JP")); // 2023/9/27 12:30:00
```

### 30.2.26 Date.prototype.toLocaleTimeString

인수로 젇날한 로캘을 기준으로 Date 객체의 시간을 표현한 문자열을 반환한다. 인수를 생략한 경우 브라우저가 동작 중인 시스템의 로캘을 적용한다.

```jsx
const today = new Date("2023/9/27/12:30");

console.log(today.toString()); // Wed Sep 27 2023 12:30:00 GMT+0900 (GMT+09:00)
console.log(today.toLocaleTimeString()); // 오후 12:30:00
console.log(today.toLocaleTimeString("ko-KR")); // 오후 12:30:00
console.log(today.toLocaleTimeString("en-US")); // 12:30:00 PM
console.log(today.toLocaleTimeString("ja-JP")); // 12:30:00
```

## 30.3 Date를 활용한 시계 예제

```jsx
(function printNow() {
  const today = new Date();

  const dayNames = [
    "(월요일)",
    "(화요일)",
    "(수요일)",
    "(목요일)",
    "(금요일)",
    "(토요일)",
    "(일요일)",
  ];

  // getDay 메서드는 해당 요일(0 ~ 6)을 나타내는 정수를 반환한다.
  const day = dayNames[today.getDay()];

  const year = today.getFullYear();
  const month = today.getMonth() + 1;
  const date = today.getDate();
  let hour = today.getHours();
  let minute = today.getMinutes();
  let second = today.getSeconds();
  const ampm = hour >= 12 ? "PM" : "AM";

  // 12시간제로 변경
  hour %= 12;
  hour = hour || 12; // hour가 0이면 12를 재할당

  // 10 미만인 분과 초를 2자리로 변경
  minute = minute < 10 ? "0" + minute : minute;
  second = second < 10 ? "0" + second : second;

  const now = `${year}년 ${month}월 ${date}일 ${day} ${hour}:${minute}:${second}${ampm}`;

  console.log(now);

  // 1초마다 printNow 함수를 재귀 호출한다.
  setTimeout(printNow, 1000);
})();
```
