# 22. this

## 22.1 this 키워드

```jsx
const circle = {
  // 프로퍼티: 객체 고유의 상태 데이터
  radius: 5,
  // 메서드: 상태 데이터를 참조하고 조작하는 동작
  getDiameter() {
    // 이 메서드가 자신이 속한 객체의 프로퍼티나 다른 메서드를 참조하려면
    // 자신이 속한 객체인 circle을 참조할 수 있어야 한다.
    return 2 * circle.radius;
  },
};

console.log(circle.getDiameter());
```

객체 리터럴 방식으로 생성한 객체의 경우 메서드 내부에서 메서드 자신이 속한 객체를 카리키는 식별자를 재귀적으로 참조할 수 있다.

하지만 자기 자신이 속한 객체를 재귀적으로 참조하는 방식은 일반적이지 않으며 바람직하지도 않다.

**this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수다. this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다.**

**this가 가리키는 값, 즉 this 바인딩은 함수 호출 방식에 의해 동적으로 결정된다.**

```jsx
// 객체 리터럴
const circle = {
  redius: 5,
  getDiameter() {
    // this는 메서드를 호출한 객체를 가리킨다.
    return 2 * this.radius;
  },
};

console.log(circle.getDiameter());
```

객체 리터럴의 메서드 내부에서의 this는 메서드를 호출한 개쳋, 즉 circle을 가리킨다.

```jsx
// 생성자 함수
function Circle(radius) {
  // this는 생성자 함수가 생성할 인스턴스를 가리킨다.
  this.radius = radius;
}

Circle.prototype.getDiameter = function () {
  // this는 생성자 함수가 생성할 인스턴스를 가리킨다.
  return 2 * this.radius;
};

// 인스턴스 생성
const circle = new Circle(5);
console.log(circle.getDiameter()); // 10
```

생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킨다. 이처럼 this는 상황에 따라 가리키는 대상이 다르다.

this는 코드 어디에서든 참조 가능하다. 전역에서도 함수 내부에서도 참조할 수 있다.

strict mode가 적용된 일반 함수 내부의 this에는 undefined가 바인딩된다. 일반 함수 내부에서 this를 사용할 필요가 없기 때문이다.

## 22.2 함수 호출 방식과 this 바인딩

**this 바인딩은 함수 호출 방식, 즉 함수가 어떻게 호출되었는지에 따라 동적으로 결정된다.**

<aside>
💡 렉시컬 스코프와 this 바인딩은 결정 시기가 다르다.

함수의 상위 스코프를 결정하는 방식인 렉시컬 스코프는 함수 정의가 평가되어 함수 객체가 생성되는 시점에 상위 스코프를 결정한다. 하지만 this 바인딩은 함수 호출 시점에 결정된다.

</aside>

함수를 호출하는 방식

1. 일반 함수 호출
2. 메서드 호출
3. 생성자 함수 호출
4. Function.prototype.apply//call/bind 메서드에 의한 간접 호출

```jsx
// this 바인딩은 함수 호출 방식에 따라 동적으로 결정된다.
const foo = function () {
  console.dir(this);
};

// 동일한 함수도 다양한 방식으로 호출할 수 있다.

// 1. 일반 함수 호출
foo(); // window

// 2. 메서드 호출
const obj = { foo };
obj.foo(); // obj

// 3. 생성자 함수 호출
new foo(); // foo {}

// 4. Function.prototype.apply/call/bind
const bar = { name: "hihi" };
foo.call(bar); // { name: 'hihi' }
foo.apply(bar); // { name: 'hihi' }
foo.bind(bar)(); // { name: 'hihi' }
```

### 22.2.1 일반 함수 호출

**기본적으로 this에는 전역 객체가 바인딩된다.**

```jsx
function foo() {
  console.log("foo's this: ", this); // window
  function bar() {
    console.log("bar's this: ", this); // window
  }
  bar();
}
foo();
```

일반 함수로 호출하면 함수 내부의 this에는 전역 객체가 바인딩된다. 자기 참조 변수이므로 객체를 생성하지 않는 일반함수에서 this는 의미가 없다.

따라서 strict mode가 적용된 일반 함수 내부의 this에는 undefined가 바인딩된다.

```jsx
// var 키워드로 선언한 전역 변수 value는 전역 객체의 프로퍼티다.
var value = 1;

const obj = {
  value: 100,
  foo() {
    console.log("foo's this: ", this); // {value:100, foo: f}
    console.log("foo's this.value: ", this.value); // 100

    // 메서드 내에서 정의한 중첩 함수
    function bar() {
      console.log("bar's this: ", this); // window
      console.log("bar's this.value: ", this.value);
      1;
    }

    // 메서드 내에서 정의한 중첩 함수도 일반 함수로 호출되면 중첩 함수 내부의 this에는
    // 전역 객체가 바인딩된다.
    bar();
  },
};

obj.foo();
```

콜백 함수가 일반 함수로 호출된다면 콜백 함수 내부의 this에도 전역 객체가 바인딩된다. 어떠한 함수라도 일반 함수로 호출되면 this에 전역 객체가 바인딩된다.

화살표 함수 내의 this는 상위 스코프의 this를 가리킨다.

### 22.2.2 메서드 호출

메서드 내부의 this에는 메서드를 호출한 객체, 즉 메서드를 호출할 때 메서드 이름 앞의 마침표(.) 연산자 앞에 기술한 객체가 바인딩된다.

```jsx
const person = {
  name: "Jeong",
  getName() {
    // 메서드 내부의 this는 메서드를 호출한 객체에 바인딩된다.
    return this.name;
  },
};

// 메서드 getName을 호출한 객체는 person이다.
console.log(person.getName()); // Jeong
```

### 22.2.3 생성자 함수 호출

생성자 함수 내부의 this에는 생성자 함수가 (미래에) 생성할 인스턴스가 바인딩된다.

```jsx
// 생성자 함수
function Circle(radius) {
  // 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가진다.
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

const circle1 = new Circle(5);
const circle2 = new Circle(10);

console.log(circle1.getDiameter()); // 10
console.log(circle2.getDiameter()); // 20
```

### 22.2.4 Function.prototype.apply/call/bind 메서드에 의한 간접 호출

Fuction.prototype.apply, Function.prototype.call 메서드는 this로 사용할 객체와 인수 리스트를 인수로 전달받아 함수를 호출한다.

```jsx
function getThisBinding() {
  return this;
}

const thisArg = { a: 1 };

console.log(getThisBinding()); // window

console.log(getThisBinding.apply(thisArg, [1, 2, 3]));
// Arguments(3) [1, 2, 3, callee: f, Symbol(Symbol.iterator): f]
// {a: 1}

console.log(getThisBinding.call(thisArg, 1, 2, 3));
// Arguments(3) [1, 2, 3, callee: f, Symbol(Symbol.iterator): f]
// {a: 1}
```

**apply와 call 메서드의 본질적인 기능은 함수를 호출하는 것이다.**

apply 메서드는 호출할 함수의 인수를 배열로 묶어 전달한다. call 메서드는 호출할 함수의 인수를 쉼표로 구분한 리스트 형식으로 전달한다.

```jsx
function getThisBinding() {
  return this;
}

const thisArg = { a: 1 };

console.log(getThisBinding.bind(thisArg)); // [Function: bound getThisBinding]
console.log(getThisBinding.bind(thisArg)()); // {a: 1}
```

Function.prototype.bind 메서드는 apply와 call 메서드와 달리 함수를 호출하지 않는다.

<p align='center'>
<img src='https://github.com/bohongu/Deep-Dive-JS/assets/91203029/d8f56547-447e-404e-84bd-d4f8e54db5fa' / >
</p>
