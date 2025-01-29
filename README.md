# ✍️ 4,5장 공부 내용 정리

## 4장 객체


🎯 정리
# 자바스크립트 객체 개념 정리

### 4-1. 객체란?

객체는 여러 개의 데이터를 하나의 단위로 묶어서 관리할 수 있는 자료구조입니다. 키(key)와 값(value)으로 이루어진 프로퍼티(Property)를 가짐
객체 선언 방법:

let user = { 
  name: "John", 
  age: 30 
};

위 예제에서 name과 age가 키이며, 각각 "John"과 30이 값이다.

### 4-2. 객체 프로퍼티 접근 방법 

객체의 프로퍼티에 접근하는 방법은 두 가지가 있음

1) 점 표기법(dot notation)
console.log(user.name); // "John"

2) 대괄호 표기법(bracket notation)
console.log(user["age"]); // 30

대괄호 표기법을 사용하면 동적으로 프로퍼티 이름을 결정할 수 있음!

### 4-3. 객체 복사와 참조

자바스크립트에서 객체는 참조(reference) 타입이다. 변수에는 객체 자체가 저장되는 것이 아니라 객체가 메모리에 저장된 주소(참조값)가 저장되고, 따라서 객체를 복사하면 참조만 복사되며, 원본의 객체에 영향을 미치게 됨.

let person = { name: "Alice" };
let clone = person; // 같은 객체를 참조
clone.name = "Bob";
console.log(person.name); // "Bob"

객체를 독립적으로 복사하려면 Object.assign() 또는 전개 연산자(...)를 사용할 수 있음

let newPerson = Object.assign({}, person);
let anotherPerson = { ...person };

### 4-4. 가비지 컬렉션

자바스크립트의 메모리 관리는 자동으로 이루어지나, 사용되지 않는 객체는 가비지 컬렉터에 의해 메모리에서 제거되는 특징
객체가 더 이상 도달할 수 없는 상태가 되면(즉, 참조되지 않으면) 메모리에서 자동으로 제거됨

### 4-5. 메서드와 this

객체의 프로퍼티 값으로 함수를 정의하면 이를 메서드(method)라고 함

let user = {
  name: "Alice",
  sayHello() {
    console.log(`Hello, my name is ${this.name}`);
  }
};

user.sayHello(); // "Hello, my name is Alice"

this는 해당 메서드를 호출한 객체를 가리킴. 하지만 화살표 함수는 자신만의 this를 가지지 않으므로 일반 함수로 메서드를 정의해야하는 특징 유의

### 4-6. 생성자 함수와 new 연산자

객체를 생성할 때 매번 동일한 구조를 작성하는 것은 비효율적이므로, 생성자 함수를 사용함

function User(name, age) {
  this.name = name;
  this.age = age;
}

let user1 = new User("Alice", 25);
let user2 = new User("Bob", 30);
console.log(user1.name); // "Alice"
console.log(user2.age);  // 30

new 키워드를 사용하면 새로운 객체가 만들어지고 this가 그 객체를 가리키게 됨

### 4-7. 옵셔널 체이닝

객체의 깊은 속성을 참조할 때 프로퍼티가 존재하지 않으면 오류가 발생할 수 있음. 이를 방지하기 위해 옵셔널 체이닝(?.)을 사용하는 것

let user = {};
console.log(user.address?.street); // undefined

user.address가 존재하지 않으면 undefined를 반환하여 안전하게 접근할 수 있음!

### 4-8. 심볼(Symbol)

Symbol은 유일한 식별자를 만들기 위한 원시 데이터 타입이다.

let id = Symbol("id");
let user = { [id]: 12345 };
console.log(user[id]); // 12345

심볼형 프로퍼티는 for..in 루프에서 제외되며, Object.keys() 같은 메서드에서도 보이지 않는 특징

### 4-9. 객체를 원시형으로 변환하기

객체가 원시값으로 변환될 때 toString()과 valueOf()가 호출됨.

let user = {
  name: "Alice",
  age: 30,
  toString() {
    return this.name;
  }
};

console.log(String(user)); // "Alice"

Symbol.toPrimitive를 이용하면 변환 방식을 직접 지정할 수도 있음.

let obj = {
  value: 100,
  [Symbol.toPrimitive](hint) {
    return hint === "string" ? "객체" : this.value;
  }
};

console.log(+obj); // 100
console.log(`${obj}`); // "객체"

이처럼 객체는 특정 연산에 따라 자동 변환될 수 있음 ㅇㅇ



# 추가자료
# 개념설명 키워드
- 객체            :여러 데이터를 저장하는 키-값 쌍 구조,참조 타입	{ name: "Alice", age: 25 }
- 참조 복사       :객체를 복사하면 참조값(주소) 만 복사됨, 점 표기법/대괄호 표기법으로 프로퍼티 조작, 얕은 복사와 싶은 복사 나뉨	let user2 = user1;
- 가비지 컬렉션	  :사용되지 않는 객체를 자동 삭제	user = null;
- 메서드와 this	  :객체 내부의 함수에서 this는 객체 자신을 가리킴, 실행 컨텍스트에 따라 달라질 수 있음 this.name
- new 생성자 함수	:같은 구조의 객체를 쉽게 생성	new User("Alice", 25)
- 옵셔널 체이닝 ?. :존재하지 않는 속성 접근 시 에러 방지, 안전하게 프로퍼티에 접근 가능	user?.address?.street
- 심볼형          :충돌 방지 고유한 키 값	let id = Symbol("id");
- 객체 변환	      :toString()을 사용해 객체를 원시값으로 변환, toString(), valueOf(), Symbol.toPrimitive를 이용해 직접 변환 로직을 설정 user.toString()


1. JS는 객체 기반 프로그래밍 언어

- 원시 타입: 단 하나의 값만 나타냄, 변경 불가
- 객체 타입: 다양한 타입의 값을 하나의 단위로 구성한 자료구조, 변경 가능한 값

2. 객체 구성: 프로퍼티 키, 프로퍼티 값 -> 프로퍼티의 집합

- 모든 값은 프로퍼티 값이 될 수 있음
- 프로퍼티 값이 함수일 경우 메서드

```js
var counter = {
  // 프로퍼티: 객체의 상태를 나타내는 값
  num: 0,
  // 메서드: 프로퍼티를 참조하고 조작할 수 있는 동작
  increase: function () {
    this.num++;
  },
};
```

### 4-2. 객체 리터럴에 의한 객체 생성

1. 클래스 기반 객체지향 언어

- 사전에 클래스를 생성하고 new + 생성자로 인스턴스 생성하는 방식으로 객체 생성
- C++, JAVA

2. 프로토타입 기반 객체지향 언어 (JS)

- 다양한 객체 생성 방법 지원
  - 객체 리터럴: 가장 기본적, 유연하고 강력함, new 연산자 + 생성자 X, 동적 프로퍼티 추가 등..
  - (Object) 생성자 함수, Object.create, 클래스 ..

3. 변수 할당 시점에 객체 리터럴이 해석되어 객체를 생성함

### 4-3. 프로퍼티

- 프로퍼티 키: 모든 문자열 또는 심벌 값
  - 빈 문자열 포함 but 키의 역할을 하지 못함
  - 암묵적 타입 변환으로 문자열이 됨
  - 중복 키 선언 시 에러 발생하지 않고 기존 프로퍼티를 덮어씀
- 프로퍼티 값: 자바스크립트에서 사용할 수 있는 모든 값

### 4-4. 메서드

함수는 객체 -> 함수는 값 -> 프로퍼티 값 사용 가능 -> 메서드: 객체에 묶여있는 함수

```js
var circle = {
  radius: 5, // ← 프로퍼티

  // 원의 지름
  getDiameter: function () {
    // ← 메서드
    return 2 * this.radius; // this는 circle을 가리키는 참조변수
  },
};

console.log(circle.getDiameter()); // 10
```

### 4-5. 프로퍼티 접근

- 객체에 존재하지 않는 key 접근 시 `undefined` 반환, ReferenceError 발생 X

### 4-6. 프로퍼티 삭제

- `delete` 연산자: 존재하지 않는 프로퍼티 삭제 시 에러 없이 무시됨

### 4-7. 객체 리터럴 확장 기능

- 프로퍼티 키 동적 생성

  1. ES5 이전: 객체 외부에서 프로퍼티 키 동적 생성
  2. ES6 이후: 객체 내부에서 프로퍼티 키 동적 생성 가능

- 메서드 축약 표현
  1. ES5 이전: 메서드 정의 시 프로퍼티 값으로 함수 할당
  2. ES6 이후: 메서드 정의 시 function 생략 가능 -> 프로퍼티에 할당한 함수와 다르게 동작함

```js
// ES6
const obj = {
  name: "Lee",
  // 메서드 축약 표현
  sayHi() {
    console.log("Hi! " + this.name);
  },
};

obj.sayHi(); // Hi! Lee
```

---

## 5장 원시 값과 객체의 비교

원시 값과 객체는 크게 세 가지 측면에서 다르다 -> 변경 여부, 메모리 공간에 저장되는 값, 변수 할당 시 전달되는 형태

### 5-1. 원시 값

1. 변경 불가능한 값 (읽기 전용)

- 데이터의 신뢰성 보장
- 값의 불변성
  - 원시 값을 할당한 변수에 원시 값을 재할당하면 -> 원시 값은 변경 불가능하므로, 새로운 메모리 공간 확보하여 값을 저장한 후 변수에 새롭게 할당한 원시 값을 가리킴 (메모리 공간 주소를 바꿈)
  - 만약 변경 가능하다면, 주소는 그대로고 주소 안의 값이 변경되었을 것 -> 즉 원시 값을 할당한 변수는 재할당이 변수 값을 변경하는 유일한 방법

2. 문자열과 불변성

- JS에서 문자열은 원시 타입이며 변경 불가함.
- 문자열은 유사 배열 객체 및 이터러블 -> 배열과 유사하게 각 문자에 접근할 수 있지만 변경 불가

```js
var str = "string";

// 문자열은 유사 배열이므로 배열과 유사하게 인덱스를 사용해 각 문자에 접근할 수 있다.
// 하지만 문자열은 원시값이므로 변경할 수 없다. 이때 에러가 발생하지 않는다.
str[0] = "S";

console.log(str); // string
```

- 값에 의한 전달

- 변수에 원시 값 변수를 할당 시 할당 되는 원시 값이 복사되어 전달 -> 값에 의한 전달
- 변수들은 같은 값을 가지나, 값은 서로 다른 메모리에 저장된 별개의 값임. **할당 후 서로 영향을 주지 않음**
- 엄밀히 하자면 메모리 주소가 전달되는 것!

```js
var score = 80;

// copy 변수에는 score 변수의 값 80이 복사되어 할당된다.
var copy = score;

console.log(score, copy); // 80  80
console.log(score === copy); // true

// score 변수와 copy 변수의 값은 다른 메모리 공간에 저장된 별개의 값이다.
// 따라서 score 변수의 값을 변경해도 copy 변수의 값에는 어떠한 영향도 주지 않는다.
score = 100;

console.log(score, copy); // 100  80
console.log(score === copy); // false
```

### 5-2. 객체

- 원시 값처럼 메모리 공간 크기 사전 정의 불가: 프로퍼티가 동적이므로
- 객체 생성 및 관리는 복잡하고 비용이 많이 들어 변경 가능한 값으로 설계하여 단점을 완화시킴
  - 여러 개의 식별자가 하나의 객체 공유 가능해서 부작용할 수 있음

1. 변경 가능한 값

- 객체(참조) 타입의 값은 변경 가능함
- 원시 값 할당 변수의 메모리 주소를 따라가면 원시 값 자체를 값으로 가짐
- 객체 값 할당 변수의 메모리 주소를 따라가면 참조 값에 접근함 -> 그 값이 저장되어 있는 주소를 가짐 -> 참조하여 실제 객체에 접근
- 재할당 없이 프로퍼티 동적 추가, 삭제, 변경 가능 -> 변수의 참조 값은 변경되지 않음

```js
/**
 * - 얕은 복사: 한 단계까지 복사 (원시 값)
 * - 깊은 복사: 중첩된 객체까지 모두 복사본을 만듦 (객체)
 */

const o = { x: { y: 1 } };

// 얕은 복사
const c1 = { ...o }; // 35장 "스프레드 문법" 참고
console.log(c1 === o); // false
console.log(c1.x === o.x); // true

// lodash의 cloneDeep을 사용한 깊은 복사
// "npm install lodash"로 lodash를 설치한 후, Node.js 환경에서 실행
const _ = require("lodash");
// 깊은 복사
const c2 = _.cloneDeep(o);
console.log(c2 === o); // false
console.log(c2.x === o.x); // false
```

+ 참조에 의한 전달

- 객체 변수를 할당하면 원본의 참조 값이 복사되어 전달 -> 참조에 의한 전달
- 여러 개의 객체가 하나의 객체 공유 가능 -> 프로퍼티 변경 시 서로 영향을 받음


1. 생성자 함수 예제 :
User라는 생성자 함수를 작성하여 새 사용자 객체를 만들 수 있을까?

# << 힌트 >>
new User(name, age)를 호출하면 { name, age } 객체가 생성되어야 함,
user1과 user2를 만들어 각각 "Tom", 25, "Jane", 30을 저장해야 함

// 생성자 함수 User를 작성하세요

let user1 = new User("Tom", 25);
let user2 = new User("Jane", 30);

console.log(user1); // { name: "Tom", age: 25 }
console.log(user2); // { name: "Jane", age: 30 }




-------------------------------------------------------------








#[정답 코드]
function User(name, age) {
  this.name = name;
  this.age = age;
}

// 객체 생성
let user1 = new User("Tom", 25);
let user2 = new User("Jane", 30);

console.log(user1); // { name: "Tom", age: 25 }
console.log(user2); // { name: "Jane", age: 30 }

생성자 함수는 함수 이름을 대문자로 시작한다는 포인트
this.name = name, this.age = age와 같이 인자로 받은 값을 객체 프로퍼티에 저장해야 하며,
new 키워드를 사용해 새로운 객체가 생성, 여기서 this는 해당 객체를 가리킴

----------------------------------------------------------------



2. 겍체의 원시값 변환 예제:
객체 product를 정의하고, toString 메서드를 추가하면?

product.toString()을 호출하면 "상품: Laptop, 가격: 1000" 형식의 문자열이 반환되도록 만들어보세요!

let product = {
  name: "Laptop",
  price: 1000,
  // 여기에 toString 메서드를 추가해보세요
};

console.log(product.toString()); // "상품: Laptop, 가격: 1000"

-----------------------------------------------------------------









#[정답 코드]

let product = {
  name: "Laptop",
  price: 1000,
  toString() {
    return `상품: ${this.name}, 가격: ${this.price}`;
  }
};

console.log(product.toString()); // "상품: Laptop, 가격: 1000"

toString 메서드를 객체에 추가하고,
this.name과 this.price를 사용하여 문자열을 만든다음
return을 사용해 원하는 문자열을 반환하는 구조로 만든다!






# 5장 개념정리
## -자료구조와 자료형 



1.이터러블(iterator) 구현 예제 문제 :
아래 numberList 객체는 숫자들의 리스트를 가지고 있습니다.
하지만 for..of 반복문을 사용하려고 하면 에러가 발생합니다.

numberList를 **이터러블(iterable)**로 만들어서 for..of 반복문이 정상적으로 작동하도록 수정해볼까요?!

const numberList = {
  numbers: [1, 2, 3, 4, 5],
};

// 수정 후에 아래 코드가 정상 작동해야 하도록 만들어보세요!
for (const num of numberList) {
  console.log(num);
}

# <<힌트>>
  Symbol.iterator 메서드를 구현해야 하며,
  next() 메서드는 { value, done } 객체를 반환해야해요
  done: true가 되면 반복이 멈춰야합니다


-------------------------------------------------







# [정답 코드] --> 수정본
const numberList = {
  numbers: [1, 2, 3, 4, 5], // 배열로 숫자 목록을 저장

  [Symbol.iterator]() {
    let index = 0; // 현재 위치를 저장하는 변수
    let numbers = this.numbers; // this를 변수에 저장하여 안전하게 접근

    return {
      next() {
        if (index < numbers.length) {
          return { value: numbers[index++], done: false }; // 다음 값 반환
        } else {
          return { done: true }; // 더 이상 값이 없으면 종료
        }
      }
    };
  }
};




2. 배열 과제 문제(복습):
확장 가능한 계산기
중요도: 5
기능을 "확장"할 수 있는 계산기 객체를 만들어 주는 생성자 함수 Calculator를 작성해봅시다.

Calculator는 두 단계를 거쳐 만들 수 있습니다.

첫 번째 단계는 "1 + 2"와 같은 문자열을 받아서 “숫자 연산자 숫자” 형태(공백으로 구분)로 바꿔주는 메서드 calculate(str)를 구현하는 것입니다. 이 함수는 +와 -를 처리할 수 있어야 하고, 연산 결과를 반환해야 합니다.

예시:

let calc = new Calculator;

alert( calc.calculate("3 + 7") ); // 10
두 번째 단계는 계산기가 새로운 연산을 학습할 수 있도록 해주는 메서드 addMethod(name, func)를 추가해 주는 것입니다. 연산자 이름을 나타내는 name과 인수가 두개인 익명 함수 func(a,b)를 받는 새 메서드를 구현해야 하죠.

구현된 메서드를 이용해 곱셈 *과 나눗셈 /, 거듭제곱 **연산자를 추가해주는 예시는 아래와 같습니다.

let powerCalc = new Calculator;
powerCalc.addMethod("*", (a, b) => a * b);
powerCalc.addMethod("/", (a, b) => a / b);
powerCalc.addMethod("**", (a, b) => a ** b);

let result = powerCalc.calculate("2 ** 3");
alert( result ); // 8


참고사항:
괄호나 복잡한 표현식 없이도 본 과제를 풀 수 있습니다.
숫자와 연산자는 공백 하나로 구분합니다.
에러 핸들링을 위한 코드를 추가해도 좋습니다(선택 사항).




------------------------------------------------------------



# << 정답 코드>> --> 활용본
function Calculator() {
  this.methods = {
    "+": (a, b) => a + b,
    "-": (a, b) => a - b
  };

  this.calculate = function (str) {
    let parts = str.split(" ");
    if (parts.length !== 3) {
      throw new Error("입력 형식이 잘못되었습니다. '숫자 연산자 숫자' 형태로 입력하세요.");
    }

    let num1 = parseFloat(parts[0]);
    let operator = parts[1];
    let num2 = parseFloat(parts[2]);

    if (isNaN(num1) || isNaN(num2)) {
      throw new Error("올바른 숫자를 입력하세요.");
    }

    if (!this.methods[operator]) {
      throw new Error("지원하지 않는 연산자입니다.");
    }

    return this.methods[operator](num1, num2);
  };

  this.addMethod = function (name, func) {
    this.methods[name] = func;
  };
}


function test() {
  console.log(x);
  var x = 5;
  console.log(x);
}

test();

