### var, let, const는 JS에서 변수를 선언하는 세가지 방법입니다.

## TDZ

- TDZ(Temporal Dead Zone)는 해석하면 " 일시적 사각지대 "
- 변수가 선언되고 변수의 초기화가 이루어지기 전까지의 구간

![IMG_0097](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdAUOcV%2FbtrlerbSm1G%2F95zpe8AgZWXj71QfWxSBJk%2Fimg.jpg)

## TDZ의 영향을 받는 구문

1. const 변수

```javascript
❌
console.log(cat)

const cat = "야옹"
//error : ReferenceError
👍
const cat = "야옹"
console.log(cat)

// 출력 : 야옹
```

2. let 변수

```javascript
❌
count;

let count;

count = 10;
//error : ReferenceError
👍
let count;

count; // => undefined

count = 10;

count; // => 10
```

3. class 구문

```javascript
❌
const myCar = new cat('mimi')

class cat {
  constructor(name) {
    this.name = name;
  }

}
//error : ReferenceError
👍
class cat {
  constructor(name) {
    this.name = name;
  }
}
const myCat = new cat('mimi')

console.log(myCat.name) // => mimi
```

## TDZ의 영향을 받지 않는 구문

- var, function( 함수 선언식 ), import

```javascript
// Works!
value; // => undefined
var value;
// Works!
hello("Shin"); // "Hello Shin :)"

function hello(name) {
  return `Hello ${name} :)`;
}
hello("Shin"); // "Hello Shin :)"
```

## 스코프

- 변수에 접근 할 수 있는 범위
- 모든 식별자는 자신이 선언된 위치에 의해 다른 코드가 식별자 자신을 참조할 수 있는 유효 범위가 결정된다. 이를 스코프라고 한다.

<br>

## 렉시컬 스코프

- 함수를 어디서 호출하는지가 아니라 어디에 선언하였는지에 따라 결정

<br>

## 스코프 체인

- 전역 변수와 지역 변수 관계에서 `스코프 체인` 개념이 나온다.

```javascript
var name = "zero";
function outer() {
  console.log("외부", name);
  function inner() {
    var enemy = "nero";
    console.log("내부", name);
  }
  inner();
}
outer();
console.log(enemy); // undefined
```

- inner 함수는 name 변수를 찾기 위해 자기 자신의 스코프에서 찾고, 없으면 한 단계 올라가 outer 스코프에서 찾고, 없으면 다시 올라가 결국 전역 스코프에서 찾는다.
- 이처럼 꼬리를 물고 계속 범위를 넓히면서 찾는 관계를 `스코프 체인` 이라 한다.

<br>

### 전역스코프와 전역 변수

- 가장 바깥 영역 스코프를 `전역 스코프`라고 불리우며, <br>
  전역 스코프에서 선언한 변수는 `전역 변수` 라고 불리운다.
- 전역 변수는 어디서든 참조가 가능하다.

<br>

### 지역 스코프와 지역 변수

- 전역이 아닌 안쪽 영역, 즉 다른 스코프는 `지역스코프` 라고 불리며, <br>
  지역 스코프에서 선언한 변수는 `지역 변수` 라고 불리운다.
- 코드의 안쪽 영역으로 블록 안, 함수 내에서만 참조 가능하다.
- 지역 변수는 전역 변수보다 더 높은 우선 순위를 가진다.

![IMG_0097](https://user-images.githubusercontent.com/98936928/185575227-17b73277-9408-41ed-b604-dc60dc147eff.jpg)

<br>

# 함수 스코프 VS 블록 스코프(화살표 함수 포함)

## 함수 스코프

- 새로운 함수가 생성 될 때마다 새로운 스코프가 발생
  - 함수 몸체에 선언한 변수는 해당 함수 안에서만 접근이 가능
- 함수 스코프 => 지역 스코프

```javascript
if (5 > 4) {
  var secret = "12345";
}
secret; // '12345'
```

- 함수가 선언되지 않아서 새로운 환경, 새로운 스코프가 형성되지 않음
- 스코프가 형성되지 않으므로 동일한 실행컨텍스트 내에서 존재
- 어디서나 secret 변수에 접근이 가능

<br>

```javascript
function a() {
  var secret = "12345";
}
secret; // undefined
```

- 이 경우 함수 생성과 동시에 a함수에 대해 새로운 실행 컨텍스트가 생성
- 실행 컨텍스트 내부에 존재하는 변수환경에 secret 변수가 저장
- secret에 접근 할 경우 스코프가 다르기에 접근 불가능

<br>

## 블록 스코프

- {} 이 생성 될 때마다 새로운 스코프가 생성
- let과 const 키워드의 등장으로 블록 스코프를 형성하는 것도 가능

```javascript
function loop() {
  for (var i = 0; i < 5; i++) {
    console.log(i);
  }
  console.log("final", i);
}
loop();
/*
	0
	1
	2
	3
	4
	final 5
*/
```

- for문 안에 변수 i를 var 키워드로 초기화
- 둘다 문제없이 console.log( i ) 에 접근이 가능

<br>

```javascript
function loop() {
  for (let i = 0; i < 5; i++) {
    console.log(i);
  }
  console.log("final", i);
}
loop(); /* "i" is not defined */
```

- 반면 i를 let으로 선언할 경우 달라진다
- let 으로 선언한 순간 변수 i는 for문 내에서만 종속되며, for문 외부에서는 i 접근이 불가능

## var

1. ES6 이전에 사용되던 변수 선언 방법
2. 함수 스코프를 가지며, 변수가 선언된 함수 내에서만 접근 가능
3. 중복선언이 가능하며, 변수 재할당이 가능
4. 호이스팅이 발생하여 선언 전에도 참조 가능

```javascript
var x = 1;
function foo() {
  var x = 2;
  console.log(x); // 2
}
console.log(x); // 1
```

💣 이처럼 var의 문제는 중복 선언을 하여도 에러를 반환하지 않아서 문제가 생긴다 💣 <br>
💣 호이스팅 떄문인데, var는 함수 스코프를 가지기 때문에 코드 전체의 최상단이 아닌 함수 내부의 최상단으로 이동 한다. 💣 <br>
💣 for문에서도 문제점이 나타난다. for문이 종료 되어도 접근이 가능해지기 때문이다. 💣

<br>

### 호이스팅

- 코드가 실행하기 전 변수와 함수선언 이 해당 스코프의 최상단으로 끌어 올려진 것 같은 현상
- JS 코드를 실행하기 전 실행 가능한 코드를 형상화 하고 구분하는 과정을 거친다.
- 여기서 구분하는 과정은 실행 컨텍스트를 위한 과정
- `실행 컨텍스트`는 실행 가능한 코드가 실행 되기 위한 필요한 환경을 의미

### 호이스팅 순서

1. 코드 실행 전, 변수와 함수의 선언 부분이 메모리에 먼저 할당
2. 변수와 함수의 할당 부분은 아직 메모리에 할당되지 않으므로 undefined 값이 할당
3. 코드가 실행 될 때, 할당된 값을 기준으로 변수와 함수가 실제로 사용

<br>

## let

1. ES6에서 추가된 블록 스코프를 가지는 변수 선언 방법
2. 변수를 선언한 블록 내에서만 접근 가능
3. 중복 선언이 불가능하며, 변수 재할당이 가능
4. 호이스팅이 발생하지 않음

```javascript
let x = 1;
if (true) {
  let x = 2;
  console.log(x); // 2
}
console.log(x); // 1
```

<br>

## const

1. let과 동일하게 블록 스코프를 가지며, 변수를 선언한 블록 내에서만 접근이 가능
2. 중복선언이 불가능하며, 변수 재할당이 불가능
3. 상수를 선언할 때 사용

```javascript
const x = 1;
// x = 2; // TypeError: Assignment to constant variable.
```

## 😈 일반적으로 변수를 선언할 때는 const를 사용하며, 변수의 값이 변해야 하는 경우 let을 사용
