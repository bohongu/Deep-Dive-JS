# 29.  Math

## 29.1 Math 프로퍼티

### 29.1.1 Math.PI

원주율 PI값을 반환한다.

```jsx
Math.PI // 3.141592653589793
```

## 29.2 Math 메서드

### 29.2.1 Math.abs

인수로 전달된 숫자의 절대값을 반환한다. 절대값은 반드시 0 또는 양수이어야 한다.

```jsx
Math.abs(-1); // 1
Math.abs("-1"); // 1
Math.abs(undefined); // NaN
Math.abs(); // NaN
```

### 29.2.2 Math.round

인수로 전달된 숫자의 소수점 이하를 반올림한 정수를 반환한다.

```jsx
Math.round(1.4); // 1
Math.round(1.6); // 2
Math.round(-1.4); // -1
Math.round(-1.6); // -2
```

### 29.2.3 Math.ceil

인수로 전달된 숫자의 소수점 이하를 올림한 정수를 반환한다. 소수점 이하를 올림하면 더 큰 정수가 된다.

```jsx
Math.ceil(1.4); // 2
Math.ceil(1.6); // 2
Math.ceil(-1.4); // -1
Math.ceil(-1.6); // -1
```

### 29.2.4 Math.floor

인수로 전달된 숫자의 소수점 이하를 내림한 정수를 반환한다. 즉, Math.ceil 메서드의 반대 개념이다.

```jsx
Math.floor(1.9); // 1
Math.floor(9.1); // 9
Math.floor(-1.9); // -2
Math.floor(-9.1); // -10
```

### 29.2.5 Math.sqrt

인수로 전달된 숫자의 제곱근을 반환한다.

```jsx
Math.sqrt(9); // 3
Math.sqrt(-9); // NaN
Math.sqrt(2); // 1.414213562373095
Math.sqrt(1); // 1
```

### 29.2.6 Math.random

임의의 난수(랜덤 숫자)를 반환한다. Math.random 메서드가 반환한 난수는 0에서 1미만의 실수다. 즉, 0은 포함되지만 1은 포함되지 않는다.

```
Math.random(); // 0에서 1 미만의 랜덤 실수

const random = Math.floor(Math.random() * 10 + 1);
console.log(random); // 1에서 10 범위의 정수
```

### 29.2.7 Math.pow

첫 번째 인수를 밑으로, 두 번째 인수를 지수로 거듭제곤한 결과를 반환한다.

```jsx
Math.pow(2, 8); // 256
Math.pow(2, -1); // 0.5
Math.pow(2); // NaN
```

### 29.2.8 Math.max

전달받은 인수 중에서 가장 큰 수를 반환한다. 인수가 전달되지 않으면 -Infinity를 반환한다.

```jsx
Math.max(1); // 1
Math.max(1, 2); // 2
Math.max(1, 2, 3); // 3
Math.max(); // -Infinity
```

### 29.2.9 Math.min

전달받은 인수 중에서 가장 작은 수를 반환한다. 인수가 전달되지 않으면 Infinity를 반환한다.

```jsx
Math.min(1); // 1
Math.min(1, 2); // 1
Math.min(1, 2, 3); // 1
Math.min(); // Infinity
```