# 28. Number

## 28.1 Number 생성자 함수

Number 생성자 함수에 인수를 전달하지 않고 new 연산자와 함께 호출하면 [[NumberData]] 내부 슬롯에 0을 할당한 Number 래퍼 객체를 생성한다.

```jsx
const numObj = new Number();
console.log(numObj); // Number {[[PrimitiveValue]]: 0 }
```

Number 생성자 함수의 인수로 숫자를 전달하면서 new 연산자와 함께 호출하면 [[NumberData]] 내부 슬롯에 인수로 전달받은 숫자를 할당한 Number 래퍼 객체를 생성한다.

```jsx
const numObj = new Number(10);
console.log(numObj); // Number {[[PrimitiveValue]]: 10 }
```

## 28.2 Number 프로퍼티

### 28.2.1 Number.EPSILON

ES6에서 도입된 Number.EPSILON은 1과 1보다 큰 숫자 중에서 가장 작은 숫자와의 차이와 같다.

```jsx
0.1 + 0.2; // 0.30000000000000004
0.1 + 0.2 === 0.3; // false
```

Number.EPSILON은 부동소수점으로 인해 발생하는 오차를 해결하기 위해 사용한다.

```jsx
function isEqual(a, b) {
  // a와 b를 뺀 값의 절대값이 Number.EPSILON보다 작으면 같은 수로 인정한다.
  return Math.abs(a - b) < Number.EPSILON;
}

isEqual(0.1 + 0.2, 0.3); // true
```

### 28.2.2 Number.MAX_VALUE

Number.MAX_VALUE는 자바스크립트에서 표현할 수 있는 가장 큰 양수 값이다. Number.MAX_VALUE보다 큰 숫자는 Infinity다.

```jsx
console.log(Number.MAX_VALUE); // 1.7976931348623157e+308
Infinity > Number.MAX_VALUE; // true
```

### 28.2.3 Number.MIN_VALUE

Number.MIN_VALUE는 자바스크립트에서 표현할 수 있는 가장 작은 양수 값이다. Nuber.MIN_VALUE보다 작은 숫자는 0이다.

```jsx
console.log(Number.MIN_VALUE); // 5e-324
Number.MIN_VALUE > 0; // true
```

### 28.2.4 Number.MAX_SAFE_INTEGER

Number.MAX_SAFE_INTEGER는 자바스크립트에서 안전하게 표현할 수 있는 가장 큰 정수값이다.

```jsx
console.log(Number.MAX_SAFE_INTEGER); *// 9007199254740991*
```

### 28.2.5 Number.MIN_SAFE_INTEGER

Number.MIN_SAFE_INTEGER는 자바스크립트에서 가장 안전하게 표현할 수 있는 가장 작은 정수값이다.

```jsx
console.log(Number.MIN_SAFE_INTEGER); *// -9007199254740991*
```

### 28.2.6 Number.POSITIVE_INFINITY

Number.POSITIVE_INFINITY는 양의 무한대를 나타내는 숫자값 Infinity와 같다.

```jsx
console.log(Number.POSITIVE_INFINITY); // Infinity
```

### 28.2.7 Number.NEGATIVE_INFINITY

Number.NEGATIVE_INFINITY는 음의 무한대를 나타내는 숫자값 -Infinity와 같다.

```jsx
console.log(Number.NEGATIVE_INFINITY); // -Infinity
```

### 28.2.8 Number.NaN

Number.NaN은 숫자가 아님을 나타내는 숫자값이다.

```jsx
console.log(Number.NaN); *// NaN*
```

## 28.3 Number 메서드

### 28.3.1 Number.isFinite

ES6에서 도입된 Number.isFinite 정적 메서드는 인수로 전달된 숫자값이 정상적인 유한수, 즉 Infinity 또는 -Infinity가 아닌지 검사하여 그 결과를 불리언 값으로 반환한다. 전달받은 인수를 숫자로 암묵적 타입 변환하지 않는다. 따라서 숫자가 아닌 인수가 주어졌을 때 반환값은 언제나 false다.

```jsx
Number.isFinite(0); // true

Number.isFinite(Infinity); // false
```

### 28.3.2 Number.isInteger

ES6에서 도입된 Number.isInteger 정적 메서드는 인수로 전달된 숫자값이 정수인지 검사하여 그 결과를 불리언 값으로 반환한다. 검사하기 전에 인수를 숫자로 암묵적 타입 변환하지 않는다.

```jsx
Number.isInteger(0); // true

Number.isInteger(0.5); // false

Number.isInteger("123"); // false
```

### 28.3.3 Number.isNaN

ES6에서 도입된 Number.isNaN 정적 메서드는 인수로 전달된 숫자값이 NaN인지 검사하여 그 결과를 불리언 값으로 반환한다. 전달받은 이수를 숫자로 암묵적 타입 변환하지 않는다.

```jsx
Number.isNaN(NaN); // true
```

### 28.3.4 Number.isSafeInteger

ES6에서 도입된 Number.isSafeInteger 정적 메서드는 인수로 전달된 숫자값이 안전한 정수 인지 검사하여 그 결과를 불리언 값으로 반환한다. 안전한 정수값은 -(2^53 - 1) 과 2^53 - 1 사이의 정수값이다. 검사전에 인수를 숫자로 암묵적 타입 변환하지 않는다.

```jsx
Number.isSafeInteger(0); // true

Number.isSafeInteger(1000000000000000); // true

Number.isSafeInteger(10000000000000001); // false

Number.isSafeInteger(0.5); // false
```

### 28.3.5 Number.prototype.toExponential

toExponential 메서드는 숫자를 지수 표기법으로 변환하여 문자열로 반환한다. 지수 표기법이란 매우 크거나 작은 숫자를 표기할 때 주로 사용하며 e앞에 있는 숫자에 10의 n승을 곱하는 형식으로 수를 나타내는 방식이다. 인수로 소수점 이하로 표현할 자릿수를 전달할 수 있다.

```jsx
(77.1234).toExponential(); // "7.71234e+1"
(77.1234).toExponential(4); // "7.7123e+1"
(77.1234).toExponential(2); // "7.71e+1"
```

### 28.3.6 Number.prototype.toFixed

toFixed 메서드는 숫자를 반올림하여 문자열로 반환한다.

```jsx
// 소수점 이하 반올림. 인수를 생략하면 기본값이 0이 지정된다.
(12345.6789).toFixed(); // "12346"

// 소수점 이하 1자릿수 유효, 나머지 반올림
(12345.6789).toFixed(1); // "12345.7"

// 소수점 이하 2자릿수 유효, 나머지 반올림
(12345.6789).toFixed(2); // "12345.68"

// 소수점 이하 3자릿수 유효, 나머지 반올림
(12345.6789).toFixed(3); //"12345.679"
```

### 28.3.7 Number.prototype.toPrecision

toPrecision 메서드는 인수로 전달받은 전체 자릿수가 유효하도록 나머지 자릿수를 반올림하여 문자열로 반환한다.

```jsx
// 전체 자릿수 유효. 인수를 생략하면 기본값이 0이 지정된다.
(12345.6789).toPrecision(); // "12345.6789"

// 전체 1자릿수 유효, 나머지 반올림
(12345.6789).toPrecision(1); // "1e+4"

// 전체 2자릿수 유효, 나머지 반올림
(12345.6789).toPrecision(2); // "1.2e+4"

// 전체 6자릿수 유효, 나머지 반올림
(12345.6789).toPrecision(6); // "12345.7"
```

### 28.3.8 Number.prototype.toString

toString 메서드는 숫자를 문자열로 변환하여 반환한다. 진법을 나타내는 2~36 사이의 정수값을 인수로 전달할 수 있다.

```jsx
// 인수를 생략하면 10진수 문자열을 반환한다.
(10).toString(); // "10"

// 2진수 문자열을 반환한다.
(16).toString(2); // "10000"

// 8진수 문자열을 반환한다.
(16).toString(8); // "20"

// 16진수 문자열을 반환한다.
(16).toString(16); // "10"
```
