# 31. RegExp

## 31.1 정규 표현식이란?

정규 표현식은 일정한 패턴을 가진 문자열의 집합을 표현하기 위해 사용하는 형식 언어다.

정규 표현식은 문자열 대상으로 **패턴 매칭 기능**을 제공한다. 패턴 매칭 기능이란 특정 패턴과 일치하는 문자열을 검색하거나 추출 또는 치환할 수 있는 기능을 말한다.

```jsx
// 사용자로부터 입력받은 휴대폰 전화번호
const tel = "010-1234-567팔";

// 정규 표현식 리터럴로 휴대폰 전화번호 패턴을 정의한다.
const regExp = /^\d{3}-\d{4}-\d{4}$/;

// tel이 휴대폰 전화번호 패턴에 매칭하는지 테스트(확인)한다.
regExp.test(tet); // false
```

## 31.2 정규 표현식의 생성

<p align='center'>
<img src='https://github.com/bohongu/Deep-Dive-JS/assets/91203029/ace62495-b77a-428a-baa8-b1efcc8f32b6' />
</p>

정규 표현식 리터럴은 패턴과 플래그로 구성된다.

```jsx
const target = "Is this all there is?";

// 패턴: is
// 플래그: i => 대소문자를 구별하지 않고 검색한다.
const regexp = /is/i;

// test메서드는 target 문자열에 대해 정규 표현식 regexp의 패턴을 검색하여 매칭 결과를
// 불리언 값으로 반환한다.
regexp.test(target); // true
```

RegExp 생성자 함수를 사용하여 RegExp 객체를 생성할 수도 있다.

```jsx
const target = "Is this all there is?";

const regexp = new RegExp(/is/i);
// const regexp = new RegExp(/is/, 'i')

// test메서드는 target 문자열에 대해 정규 표현식 regexp의 패턴을 검색하여 매칭 결과를
// 불리언 값으로 반환한다.
regexp.test(target); // true
```

## 31.3 RegExp 메서드

### 31.3.1 RegExp.prototype.exec

exec 메서드는 인수로 전달받은 문자열에 대해 정규 표현식의 패턴을 검색하여 매칭 결과를 배열로 반환한다. 매칭 결과가 없는 경우 null을 반환한다.

```jsx
const target = "Is this all there is?";
const regExp = /is/;

console.log(regExp.exec(target));
// [ 'is', index: 5, input: 'Is this all there is?', groups: undefined ]
```

### 31.3.2 RegExp.prototype.test

test 메서드는 인수로 전달받은 문자열에 대해 정규 표현식의 패턴을 검색하여 매칭 결과를 불리언 값으로 반환한다.

```jsx
const target = "Is this all there is?";
const regExp = /is/;

console.log(regExp.test(target)); // true
```

### 31.3.3 String.prototype.match

String 표준 빌트인 객체가 제공하는 match 메서드는 대상 문자열과 인수로 전달받은 정규 표현식과의 매칭 결과를 배열로 반환한다.

```jsx
const target = "Is this all there is?";
const regExp = /is/;

console.log(target.match(regExp)); // [ 'is', index: 5, input: 'Is this all there is?', groups: undefined ]
```

exec 메서드는 문자열 내의 모든 패턴을 검색하는 g 플래그를 지정해도 첫 번째 매칭 결과만 반환하짐만 match 메서드는 g 플래그가 지정되면 모든 매칭 결과를 배열로 반환한다.

## 31.4 플래그

플래그는 총 6개 있다. 그 중 3개의 플래그가 중요하게 사용된다.

<p align='center'>
<img src='https://github.com/bohongu/Deep-Dive-JS/assets/91203029/03aa86f5-fd43-4dbb-89b8-5043289eaed4' />
</p>

플래그는 옵션이므로 선택적으로 사용할 수 있으며, 순서와 상관없이 하나 이상의 플래그를 동시에 설정할 수도 있다.

```jsx
const target = "Is this all there is?";

// target 문자열에서 is 문자열을 대소문자를 구별하여 한 번만 검색한다.
console.log(target.match(/is/));
// [ 'is', index: 5, input: 'Is this all there is?', groups: undefined ]

// target 문자열에서 is 문자열을 대소문자를 구별하지 않고 한 번만 검색한다.
console.log(target.match(/is/i));
// [ 'Is', index: 0, input: 'Is this all there is?', groups: undefined ]

// target 문자열에서 is 문자열을 대소문자를 구별하여 전역 검색한다.
console.log(target.match(/is/g));
// [ 'is', 'is' ]

// target 문자열에서 is 문자열을 대소문자를 구별하지 않고 전역 검색한다.
console.log(target.match(/is/gi));
// [ 'Is', 'is', 'is' ]
```

## 31.5 패턴

패턴은 /로 열고 닫으며 문자열의 따옴표는 생략한다. 또한 패턴은 특별한 의미를 가지는 메타문자 또는 기호로 표현할 수 있다.

### 31.5.1 문자열 검색

```jsx
const target = "Is this all there is?";

const regExp = /is/;

console.log(regExp.test(target)); // true

console.log(target.match(regExp));
// [ 'is', index: 5, input: 'Is this all there is?', groups: undefined ]
```

### 31.5.2 임의의 문자열 검색

.은 임의의 문자 한 개를 의미한다. 문자의 내용은 무엇이든 상관없다.\

```jsx
const target = "Is this all there is?";

// 임의의 3자리 문자열을 대소문자를 구별하여 전역 검색한다.
const regExp = /.../g;

console.log(target.match(regExp));
// [ 'Is ', 'thi', 's a', 'll ', 'the', 're ', 'is?' ]
```

### 31.5.3 반복 검색

{m,n}은 앞선 패턴이 최소 m번, 최대 n번 반복되는 문자열을 의미한다.

```jsx
const target = "A AA B BB Aa Bb AAA";

// 'A'가 최소 1번, 최대 2번 반복되는 문자열을 전역 검색한다.
const regExp = /A{1,2}/g;

console.log(target.match(regExp)); // [ 'A', 'AA', 'A', 'AA', 'A' ]
```

{n}은 앞선 패턴이 n번 반복되는 문자열을 의미한다. 즉, {n}은 {n,n}과 같다.

```jsx
const target = "A AA B BB Aa Bb AAA";

// 'A'가 2번 반복되는 문자열을 전역 검색한다.
const regExp = /A{2}/g;

console.log(target.match(regExp)); // [ 'AA', 'AA' ]
```

{n,}은 앞선 패턴이 최소 n번 이상 반복되는 문자열을 의미한다.

```jsx
const target = "A AA B BB Aa Bb AAA";

// 'A'가 최소 2번 이상 반복되는 문자열을 전역 검색한다.
const regExp = /A{2,}/g;

console.log(target.match(regExp)); // [ 'AA', 'AAA' ]
```

+는 앞선 패턴이 최소 한번 이상 반복되는 문자열을 의미한다. 즉, +는 {1,}과 같다.

```jsx
const target = "A AA B BB Aa Bb AAA";

// 'A'가 최소 한 번 이상 반복되는 문자열을 전역 검색한다.
const regExp = /A+/g;

console.log(target.match(regExp)); // [ 'A', 'AA', 'A', 'AAA' ]
```

?는 앞선 패턴이 최대 한 번(0번 포함) 이상 반복되는 문자열을 의미한다. 즉, ?는 {0,1}과 같다.

```jsx
const target = "color colour";

// 'colo' 다음 'u'가 최대 한 번(0번 포함) 이상 반복되고 'r'이 이어지는 문자열을 전역 검색한다.
const regExp = /colou?r/g;

console.log(target.match(regExp)); // [ 'color', 'colour' ]
```

### 31.5.4 OR 검색

!은 or의 의미를 갖는다.

```jsx
const target = "A AA B BB Aa Bb";

// 'A' 또는 'B'를 전역 검색한다.
const regExp = /A|B/g;

console.log(target.match(regExp));
// ['A', 'A', 'A', 'B', 'B', 'B', 'A', 'B']
```

분해되지 않은 단어 레벨로 검색하기 위해서는 +를 함께 사용한다.

```jsx
const target = "A AA B BB Aa Bb";

// 'A' 또는 'B'가 한 번 이상 반복되는 문자열을 전역 검색한다.
// 'A', 'AA', 'AAA', ... 또는 'B', 'BB', 'BBB'...
const regExp = /A+|B+/g;

console.log(target.match(regExp));
// [ 'A', 'AA', 'B', 'BB', 'A', 'B' ]
```

[]내의 문자는 or로 동작한다. 그 뒤에 +를 사용하면 앞선 패턴을 한 번 이상 반복한다.

```jsx
const target = "A AA B BB Aa Bb";

// 'A' 또는 'B'가 한 번 이상 반복되는 문자열을 전역 검색한다.
// 'A', 'AA', 'AAA', ... 또는 'B', 'BB', 'BBB'...
const regExp = /[AB]+/g;

console.log(target.match(regExp));
// [ 'A', 'AA', 'B', 'BB', 'A', 'B' ]
```

범위를 지정하려면 [] 내에 -를 사용한다.

```jsx
const target = "A AA B BB Aa Bb";

// 'A' ~ 'Z'가 한 번 이상 반복되는 문자열을 전역 검색한다.
// 'A', 'AA', 'AAA', ... 또는 'B', 'BB', 'BBB'... 또는 'Z', 'ZZ', ...
const regExp = /[A-Z]+/g;

console.log(target.match(regExp));
// [ 'A', 'AA', 'B', 'BB', 'A', 'B' ]
```

\d는 숫자를 의미한다. \D는 숫자가 아닌 문자를 의미한다.

```jsx
const target = "AA BB 12,345";

// '0' ~ '9' 또는 ','가 한 번 이상 반복되는 문자열을 전역 검색한다.
let regExp = /[\d,]+/g;

target.match(regExp); // ["12,345"]

// '0' ~ '9'가 아닌 문자(숫자가 아닌 문자) 또는 ','가 한 번 이상 반복되는 문자열을 전역 검색한다.
regExp = /[\D,]+/g;

target.match(regExp); // ["AA BB ", ","]
```

\w는 알파벳, 숫자, 언더스코어를 의미한다. \W는 알파벳, 숫자, 언더스코어가 아닌 문자를 의미한다.

```
const target = "Aa Bb 12,345 _$%&";

// 알파벳, 숫자, 언더스코어, ','가 한 번 이상 반복되는 문자열을 전역 검색한다.
let regExp = /[\w,]+/g;

target.match(regExp); // ["Aa", "Bb", "12,345", "_"]

// 알파벳, 숫자, 언더스코어가 아닌 문자 또는 ','가 한 번 이상 반복되는 문자열을 전역 검색한다.
regExp = /[\W,]+/g;

target.match(regExp); // [" ", " ", ",", " $%&"]
```

### 31.5.5 NOT 검색

[…] 내의 ^은 not의 의미를 갖는다.

```jsx
const target = "AA BB 12 Aa Bb";

// 숫자를 제외한 문자열을 전역 검색한다.
const regExp = /[^0-9]+/g;

console.log(target.match(regExp)); // [ 'AA BB ', ' Aa Bb' ]
```

### 31.5.6 시작 위치로 검색

[…] 밖의 ^은 문자열의 시작을 의미한다.

```jsx
const target = "https://poinemaweb.com";

// 'https'로 시작하는지 검사한다.
const regExp = /^https/;

regExp.test(target); // true
```

### 31.5.7 마지막 위치로 검색

$는 문자열의 마지막을 의미한다.

```jsx
const target = "https://poinemaweb.com";

// 'https'로 시작하는지 검사한다.
const regExp = /com$/;

regExp.test(target); // true
```

## 31.6 자주 사용하는 정규표현식

### 31.6.1 특정 단어로 시작하는지 검사

```jsx
const url = "https://example.com";

// 'http://' 또는 'https://'로 시작하는지 검사한다.
/^https?:\/\//.test(url); // true
```

### 31.6.2 특정 단어로 끝나는지 검사

```jsx
const fileName = "index.html";

// 'html'로 끝나는지 검사한다.
/html$/.test(fileName); // true
```

### 31.6.3 숫자로만 이루어진 문자열인지 검사

```jsx
const target = "12345";

// 숫자로만 이루어진 문자열인지 검사한다.
/^\d+$/.test(target); // true
```

### 31.6.4 하나 이상의 공백으로 시작하는지 검사

```jsx
const target = " Hi!";

// 하나 이상의 공백으로 시작하는지 검사한다.
/^[\s]+/.test(target); // true
```

### 31.6.5 아이디로 사용 가능한지 검사

```jsx
const id = "abc123";

// 알파벳 대소문자 또는 숫자로 시작하고 끝나며 4~10자리인지 검사한다.
/^[A-Za-z0-9]{4,10}$/.test(id); // true
```

### 31.6.6 메일 주소 형식에 맞는지 검사

```jsx
const email = "jaehong2782@gmail.com";

/^[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*\.[a-zA-Z]{2,3}$/.test(
  email
); // true
```

### 31.6.7 핸드폰 번호 형식에 맞는지 검사

```
const cellphone = "010-1234-5678";

/^\d{3}-\d{3,4}-\d{4}$/.test(cellphone); // true
```

### 31.6.8 특수 문자 포함 여부 검사

```jsx
const target = "abc#123";

/[^A-Za-z0-9]/gi.test(target); // true
```
