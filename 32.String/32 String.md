# 32. String

## 32.1 String 생성자 함수

표준 빌트인 객체인 String 객체는 생성자 함수 객체다. 따라서 new 연산자와 함께 호출하여 String 인스턴스를 생성할 수 있다.

```
const strObj = new String();
console.log(strObj); // (크롬 브라우저 개발자 도구에서 실행) String {length: 0, [[PrimitiveValue]]: ""}
```

String 생성자 함수의 인수로 문자열을 전ㄷ라하면서 new 연산자와 함께 호출하면 [[StringData]] 내부 슬롯에 인수로 전달받은 문자열을 할당한 String 래퍼 객체를 생성한다.

String 래퍼 객체는 각 문자를 프로퍼티 값으로 갖는 유사 배열 객체이면서 이터러블이다.

new 연산자를 사용하지 않고 String 생성자 함수를 호출하면 String 인스턴스가 아닌 문자열을 반환한다.

## 32.2 length 프로퍼티

length 프로퍼티는 문자열의 문자 개수를 반환한다.

```jsx
"Hello".length; // 5
"안녕하세요!".length; // 6
```

## 32.3 String 메서드

String 객체의 메서드는 언제나 새로운 문자열을 반환한다. 문자열은 변경 불가능한 원시 값이기 때문에 **String 래퍼 객체도 읽기 전용 객체로 제공된다.**

### 32.3.1 String.prototype.indexOf

대상 문자열에서 인수로 전달받은 문자열을 검색하여 첫 번째 인덱스를 반환한다. 검색에 실패하면 -1을 반환한다.

```jsx
const str = "Hello World";

// 문자열 str에서 'l'을 검색하여 첫 번째 인덱스를 반환한다.
str.indexOf("l"); // 2

// 문자열 str에서 'or'을 검색하여 첫 번째 인덱스를 반환한다.
str.indexOf("or"); // 7

// 문자열 str에서 'x'을 검색하여 첫 번째 인덱스를 반환한다. 검색에 실패하면 -1을 반환한다.
str.indexOf("x"); // -1
```

indexOf 메서드의 2번째 인수로 검색을 시작할 인덱스를 전달할 수 있다.

```jsx
// 문자열 str의 인덱스 3부터 'l'을 검색하여 첫 번째 인덱스를 반환한다.
str.indexOf("l", 3); // 3
```

### 32.3.2 String.prototype.search

대상 문자열에서 인수로 전달받은 정규 표현식과 매치하는 문자열을 검색하여 일치하는 문자열의 인덱스를 반환한다. 검색에 실패하면 -1을 반환한다.

```jsx
const str = "Hello World";

// 문자열 str에서 정규 표현식과 매치하는 문자열을 검색하여 일치하는 문자열의 인덱스를 반환한다.
str.search(/o/); // 4
str.search(/x/); // -1
```

### 32.3.3 String.prototype.includes

대상 문자열에 인수로 전달받은 문자열이 포함되어 있는지 확인하여 그 결과를 true 또는 false로 반환한다.

```jsx
const str = "Hello World";

str.includes("Hello"); // true
str.includes(""); // true
str.includes("x"); // false
str.includes(); // false
```

### 32.3.4 String.prototype.startsWith

대상 문자열이 인수로 전달받은 문자열로 시작하는지 확인하여 그 결과를 true 또는 false로 반환한다.

```jsx
const str = "Hello World";

str.startsWith("He"); // true

str.startsWith("x"); // false
```

### 32.3.5 String.prototype.endsWith

대상 문자열이 인수로 전달받은 문자열로 끝나는지 확인하여 그 결과를 true 또는 false로 반환한다.

```jsx
const str = "Hello World";

str.endsWith("ld"); // true

str.endsWith("x"); // false
```

### 32.3.6 String.prototype.charAt

대상 문자열에서 인수로 전달받은 인덱스에 위치한 문자를 검색하여 반환한다.

```jsx
const str = "Hello";

for (let i = 0; i < str.length; i++) {
  console.log(str.charAt(i)); // H e l l o
}
```

```jsx
// 인덱스가 문자열의 범위를 벗어난 경우 빈 문자열을 반환한다.
str.charAt(5); // ''
```

### 32.3.7 String.prototype.substring

대상 문자열에서 첫 번째 인수로 전달받은 인덱스에 위치하는 문자부터 두 번째 인수로 전달받은 인덱스에 위치하는 문자의 바로 이전 문자까지의 부분 문자열을 반환한다.

```jsx
const str = "Hello World";

// 인덱스 1부터 인덱스 4 이전까지의 부분 문자열을 반환한다.
str.substring(1, 4); // ell
```

<p align='center'>
<img width="361" alt="스크린샷 2023-10-07 오후 2 23 07" src="https://github.com/bohongu/Deep-Dive-JS/assets/91203029/193feb2f-8811-4818-9f16-854102674d0b">
</p>

```jsx
const str = "Hello World"; // str.length == 11

// 첫 번째 인수 > 두 번째 인수인 경우 두 인수는 교환된다.
str.substring(4, 1); // 'ell'

// 인수 < 0 또는 NaN인 경우 0으로 취급된다.
str.substring(-2); // 'Hello World'

// 인수 > 문자열의 길이인 경우 인수는 문자열의 길이로 취급된다.
str.substring(1, 100); // 'ello World'
```

### 32.3.8 String.prototype.slice

substring 메서드와 동일하게 동작한다. 단, slice 메서드에는 음수인 인수를 전달할 수 있다. 음수인 인수를 전달하면 대상 문자열의 가장 뒤에서부터 시작하여 문자열을 잘라내어 반환한다.

```jsx
const str = "hello world";

// substring과 slice 메서드는 동일하게 동작한다.
// 0번째부터 5번째 이전 문자까지 잘라내어 반환
str.substring(0, 5); // 'hello'
str.slice(0, 5); // 'hello'

// 인덱스가 2인 문자부터 마지막 문자까지 잘라내어 반환
str.substring(2); // 'llo world'
str.slice(2); // 'llo world'

// 인수 < 0 또는 NaN인 경우 0으로 취급된다.
str.substring(-5); // 'hello world'
// slice 메서드는 음수인 인수를 전달할 수 있다. 뒤에서 5자리를 잘라내어 반환한다.
str.slice(-5); // 'world'
```

### 32.3.9 String.prototype.toUpperCase

대상 문자열을 모두 대문자로 변경한 문자열을 반환한다.

```jsx
const str = "Hello World!";

str.toUpperCase(); // 'HELLO WORLD!'
```

### 32.3.10 String.prototype.toLowerCase

대상 문자열을 모두 소문자로 변경한 문자열을 반환한다.

```jsx
const str = "Hello World!";

str.toLowerCase(); // 'hello world!'
```

### 32.3.11 String.prototype.trim

대상 문자열 아뒤에 공백 문자가 있을 경우 이를 제거한 문자열을 반환한다.

String.prototype.trimStart, Stringprototype.trimEnd를 사용하면 대상 문자열 앞 또는 뒤에 공백 문자가 있을 경우 이를 제거한 문자열을 반환한다.

```jsx
const str = "  foo  ";

str.trim(); // 'foo'

str.trimStart(); // 'foo  '

str.trimEnd(); // '  foo'
```

### 32.3.12 String.prototype.repeat

대상 문자열을 인수로 전달받은 정수만큼 반복해 연결한 새로운 문자열을 반환한다. 인수로 전달받은 정수가 0이면 빈 문자열을 반환하고, 음수면 RangeError를 발생시킨다.

```jsx
const str = "abc";

str.repeat(); // ''
str.repeat(0); // ''
str.repeat(1); // 'abc'
str.repeat(2); // 'abcabc'
str.repeat(2.5); // 'abcabc' (2.5 => 2)
str.repeat(-1); // RangeError
```

### 32.3.13 String.prototype.replace

대상 문자열에서 첫 번째 인수로 전달받은 문자열 또는 정규표현식을 검색하여 두 번째 인수로 전달한 문자열로 치환한 문자열을 반환한다.

```jsx
const str = "Hello world";

// str에서 첫 번째 'world'를 검색하여 두 번째 인수 'Jeong'로 치환한다.
str.replace("world", "Jeong"); // 'Hello Jeong'
```

검색된 문자열이 여럿 존재할 경우 첫 번째로 검색된 문자열만 치환한다.

```jsx
const str = "Hello world world";

str.replace("world", "Jeong"); // 'Hello Jeong world'
```

### 32.3.14 String.prototype.split

대상 문자열에서 첫 번째 인수로 전달한 문자열 또는 정규 표현식을 검색하여 문자열을 구분한 후 분리된 각 문자열로 이루어진 배열을 반환한다.

```jsx
const str = "How are you doing?";

// 공백으로 구분(단어로 구분)하여 배열로 반환한다.
str.split(" "); // ["How", "are", "you", "doing?"]
```
