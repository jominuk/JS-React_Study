# 함수 

## 1. 함수란?

- 일련의 과정을 문으로 구현하고 크도 블록으로 감싸서 하나의 실행 단위로 정의한 것
- 하나의 특별한 목적의 작업을 수행하도록 설계된 독립적인 블록
- 함수는 입력을 받아 출력을 내보낸다. 이 때 함수 내부로 입력을 전달받은 변수를 ```매개변수```, 입력을 ```인수```, 출력을 ```반환값```
- 매개변수(parameter)란 함수를 호출할 때 인수(argument)로 전달된 값을 함수 내부에서 사용할 수 있게 해주는 변수

## 2. 함수정의

```jsx
function add(x, y) {
  return x + y;
}
```
- 함수 호출
  - 인수를 매개변수를 통해 함수에 전달하면서 함수의 실행을 명시적으로 지시 하는 것
```
//함수 호출
var result = add(2,5)

//함수 add에 인수 2,5를 전달하면서 호출하면 반환값 7을 반환한다.
console.log(result);
```

## 3. 함수를 사용하는 이유 

- 코드의 재사용이라는 측면에서 매우 유용
- 유지 보수의 편의성을 높이고 실수를 줄여 코드의 신뢰성을 높힘, 코드의 가독성을 향상

## 4. 함수 리터럴 

- 함수 리터럴은 ```function```키워드, 함수 이름, 매개 변수 목록, 함수 몸체로 구성
```jsx
//변수에 함수 리터럴을 할당
var f = function add(x, y) {
  return x + y;
};
```

## 5. 함수 정의 

### 5-1 함수 선언문
```jsx
function add(x, y) {
  return x + y;
}

// 함수명이 정의되어 있고, 별도의 할당 명령이 없는 것
```

### 5-2 함수 표현식
```jsx
var add = function (x, y) {
  return x + y;
};
// 정의한 function을 별도의 변수에 할당하는 것
// 익명 함수와 유사
```

### 5-2.1 함수 생성 시점과 함수 호이스팅

- [선언식과 표현식의 차이는 호이스팅에서 발생한다.] 
- 함수 선언식은 함수 전체를 호이스팅하며, 함수 표현식은 별도의 변수에 할당하게 되는데, 변수는 선언부와 할당부를 나누어 호이스팅 하게 됩니다.

```jsx
// 함수 참조
cosole.log(add); // f add(x y)
cosole.log(sub); // undefined

// 함수 호출
console.log(add(2,5)); // 7
console.log(sub(2,5)); // TypeError

// 함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 표현식
var sub = function (x, y) {
  return x - y;
};
```

- 함수 표현식으로 함수를 정의하면 함수 호이스팅이 발생하는 것이 아니라 변수 호이스팅이 발생한다.

### 5-3 Function 생성자 함수 

- 객체를 생성하는 함수를 말함

```jsx
var add = new Function( 'x' , 'y', 'return x + y');

console.log(add(2,5)); //7

```

- 문제점이라고 하면 함수를 생성하는 방식이 일반적이지 않으며, 바람직하지도 않다.
- ```클로저(Closure)```를 생성하지 않는 등 다른 함수들과 다른게 동작한다.

```jsx
var add 1 = (function () {
  var a = 10;
  return function( x,y ) {
    return x+y+a;
  };
}());

console.log(add 1 (1,2)); // 13


var add 2 = (function () {
  var a = 10;
  return new Function( 'x' , 'y', 'return x + y + a');
}());

console.log(add 1 (1,2)); // ReferenceError
```

### 5-4 화살표 함수 
- ES6에서 도입된 ```화살표 함수```는 function 키워드 대신 화살표를 사용해 좀 더 간략하게 함수를 선언할 수 있음.
```jsx
const add = ( x,y ) => x + y;
console.log(add(2,5)); // 7
```

## 6. 익명 함수와 선언적 함수의 차이 

- ```익명함수```는 순차적인 코드 실행에서 코드가 해당 줄을 읽을 떄 생성
- ```익명함수```는 호이스팅 시 위로 올라가지 않고 익명함수를 저장한 변수만 올라가게 되며 이를 변수 호이스팅이라 불린다.

```jsx
let 익명함수

// 익명 함수를 2번 생성
익명함수 = function () {
  console.log('1번 익명함수')
}
익명함수 = function () {
  console.log('2번 익명함수')
}

익명함수()

//실행결과
[ 2번 익명함수 ]

=======================================================


let 익명함수
익명함수()

// 익명 함수를 2번 생성
익명함수 = function () {
  console.log('1번 익명함수')
}
익명함수 = function () {
  console.log('2번 익명함수')
}

//실행결과
error

// 당연히 익명 함수는 순차적으로 실행시키기에 에러
```

- ```선언적 함수```는 순차적인 코드 실행이 일어나기 전에 생성, 따라서 같은 블록이라면 어디에서 호출해도 무방

```jsx
//선언적 함수를 호출

function 선언적함수 () {
  console.log("1번 함수")
}
function 선언적함수 () {
  console.log("2번 함수")
}

선언적 함수 ()
//실행결과
[ 2번 함수 ]

==============================================
선언적 함수 ()

function 선언적함수 () {
  console.log("1번 함수")
}
function 선언적함수 () {
  console.log("2번 함수")
}


//실행결과
[ 2번 함수 ]

```

- ```익명함수```와 ```선언적함수```를 같이 사용해본다
```jsx
함수()

함수 = function () {
  consoloe.log("익명함수입니다.")
};

function 함수 () {
  console.log("선언적함수입니다.)
};

함수()

// 출력 결과
선언적함수입니다
익명함수입니다
```
- 상단 함수()의 결과는 선언적함수를 호출하고
- 하단 함수()의 결과는 함수가 함수라는 변수 자체를 덮어쓰기 때문에 익명함수라는 결과를 출력하게 된다.


## 7. 함수 호출 

- 함수를 가리키는 식별자와 한 쌍의 소괄호인 함수 호출 연산자로 호출

### 7-1 매개변수와 인수

```jsx
function add(x,y) {
  return x + y;
}

// 함수 호출
// 인수 1과 2가 매개변수 x와 y에 순서대로 할당되고 함수 몸체의 문들이 실행된다.
```

![image](https://github.com/jominuk/JS_Study/assets/117640309/8c465c95-c850-43e8-850d-ecf81cf3214e)

### 7-1.1 매개변수

- 매개 변수는 함수 몸체 내부에서만 참조할 수 있고 함수 몸체 외부에서는 참조할 수 없다.
```jsx
function add ( x , y ) {
  console.log( x , y ); // 2 5
  return x + y;
}

add(2,5)

//add 함수의 매개변수 x,y는 함수 몸체 내부에서만 참조할 수 있다.
console.log(x,y); // ReferenceError
```

### 7-1.2 인수 확인

```jsx
function add(x,y) {
  return x + y;
}

=============================================

function add(x,y) {
  return x + y;
}
console.log(add(2));  // NaN
consoloe.log(add('a','b'));   // 'ab'
```

- 첫번 쨰 코드는 코드상으로 어떤 타입의 인수를 전달해야하는지 어떤 타입으 ㅣ값을 반환하는지 명확하지 않다
- 하지만 두번 쨰 코드는 아무 제기없이 코드를 실행한다 이유는 다음과 같다.
   - JS함수는 매개변수와 인수의 개수가 일치하는지 확인하지 않는다.
   - JS는 동적 타입 언어, 따라서 매개변수의 타입을 사전에 지정할 수 없다.

```jsx
function add (x,y) {
  if(typeof x !== 'number' || typeof y !== 'number) {
    // 매개변수를 통해 전달된 인수의 타입이 부적잘한 경우 에러를 발생
    throw new TypeError('인수는 모두 숫자 값이어야 합니다')
  }
  return x + y;
}

console.log(add2));  // TypeError
console.log(add('a','b')); // TypeError
```

- 이처럼 
```jsx

```

```jsx

```


```jsx

```


```jsx

```


```jsx

```










```jsx

```




```jsx

```































