# Scope (스코프)

## 1.스코프란?

- 변수에 접근 할 수 있는 범위
- 모든 식별자는 자신이 선언된 위치에 의해 다른 코드가 식별자 자신을 참조할 수 있는 유효 범위가 결정된다. 이를 스코프라고 한다.

```jsx
function add(x,y) {
  // 매개변수는 함수 몸체 내부에서만 참조할 수 있다.
  // 즉, 매개변수의 스코프(유효범위)는 함수 몸체 내부다.
  console.log(x,y); // 2 5
  return x + y;
}

add(2,5);

// 매개변수는 함수 몸체 내부에서만 참조할 수 있다.
console.log(x,y); // ReferenceError

===========================================================================================================

var var1 = 1; // 코드의 가장 바깥 영역에서 선언한 벼눗

if (true) {
  var var2 = 2; // 코드 블록 내에서 선언한 변수
  if(true) {
    var var3 = 3; // 중첩된 코드 블록 내에서 선언한 변수 
  }
}

function foo() {
  var var4 = 4; // 함수 내에서 선언한 변수

  function bar() {
    var var5 = 5;
  }
}

console.log(var1) // 1
console.log(var2) // 2
console.log(var3) // 3
console.log(var4) // ReferenceError : var4 is not defined
console.log(var5) // ReferenceError : var5 is not defined
```

- "코드가 어디서 실행되며 주변에 어떤 코드가 있는지"를 ```렉시컬환경```이라고 부른다
- 문맥은 ```렉시컬환경```으로 이뤄진다.
- 이를 구현한 것이 ```실행 컨텍스트```이며, 모든 코드는 ```실행 컨텍스트```에서 평가되고 실행된다.

- var키워드로 선언된 변수는 같은 스코프 내에서 중복선언이 허용된다.
- let, const키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용하지 않는다.



## 2.스코프의 종류?

| 구분 |        설명      | 스코프    | 변수     |
| ---- |        ----      | -----     | -----    |
| 전역 |코드의 가장 바깥영역| 전역 스코프| 전역 변수|
| 지역 |함수 몸체 내부     |지역 스코프  | 지역 변수|



![images_jinseoit_post_768d4117-0a6c-49c3-952c-74e663201b17_image](https://github.com/jominuk/JS_Study/assets/117640309/212263e0-9dba-4ede-81c0-2cfdb3fe6ed8)


## 2-1. global Scope 

- 전역 범위는 큰 방과 같으며 전역 범위에 정의된 변수나 함수는 다른 범위에서 코드의 어디에서나 액세스 할 수 있음.

## 2-2. Local Scope

- 큰 방 안에 작은 방이 있는 것처럼 로컬 범위 내에서 정의된 변수 또는 함수는 해당 범위 내에서만 액세스할 수 있으며, 로컬 범위를 벗어나면 더 이상 액세스할 수 없다.

## 2-3. Function Scope

```jsx
function greet() {
  var message = "Hello, there!";
  console.log(message);
}

console.log(message); // Error: ReferenceError: message is not defined
```

- 함수 생성과 동시에 greet함수에 대한 새로운 실행 컨텍스트가 생성
- 이 실행 컨텍스트 내부에 존재하는 변수환경(variable environment)에 message변수가 저장
- 함수 외부에서 message에 접근하려고 할 경우 스코프가 다르기 때문에 해당 변수에 접근이 불가능
- 함수 외부는 global scope이고, 함수 내부에 greet함수의 Local scope인데 부모 스코프는 자식 스코프에 간섭할 수 없기에 접근이 불가능

```jsx
function outer() {
  var outerVariable = "I'm outside!";

  function inner() {
    var innerVariable = "I'm inside!";
    console.log(innerVariable); // Output: I'm inside!
    console.log(outerVariable); // Output: I'm outside!
  }

  inner();
}

outer();
```

## 2-4. Function Scope

- 블록스코프는 말 그래도 블록 {}이 생성될 때마다 새로운 스코프가 형성되는 것을 의미
- 원래 자바스크립트는 함수 스코프를 따르지만, let과 const 키워드의 등장으로 블록 스코프를 형성하는 것도 가능

```jsx
function greet() {
  if (true) {
    var message = "Hello, there!";
    let blockScopedMessage = "I'm block-scoped!";
    const constantMessage = "I won't change!";
    console.log(message); // Output: Hello, there!
    console.log(blockScopedMessage); // Output: I'm block-scoped!
    console.log(constantMessage); // Output: I won't change!
  }

  console.log(message); // Output: Hello, there!
  console.log(blockScopedMessage); // Error: ReferenceError: blockScopedMessage is not defined
  console.log(constantMessage); // Error: ReferenceError: constantMessage is not defined
}

greet();

// 블록 범위 내에서 세 변수 모두의 값에 액세스하고 인쇄할 수 있지만, 블록 범위 밖에서는 변수에 대한 액세스가 다르다.
```

```jsx
function loop() {
	for(var i = 0; i < 5; i++) {
		console.log(i);
	}
	console.log('final',i);
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

===========================================================================================

function  loop() {
	for (let i = 0; i < 5; i++) {
		console.log(i);
	}
	console.log('final', i);
}
loop(); /* ReferenceError: i is not defined */

```


## 3. 스코프 체인 

- 범위 체인은 코드가 여러 수준의 중첩 범위에서 변수 및 함수에 액세스 할 수 있도록 하는 JS의 메커니즘
- scope는 식별자가 유효한 범위
- 전역 변수와 지역 변수 관계에서 스코프 체인 개념이 나온다.


![image](https://github.com/jominuk/JS_Study/assets/117640309/dbb0f3d3-6117-477c-87c1-dc7053952adf)


```jsx
function outer() {
  var x = 10;

  function inner() {
    var y = 20;
    console.log(x + y); // Accessing variables from outer scopes : 30
  }

  inner();
}

outer();
```

- 현재 코드는 outer와 inner 두개의 중첩 함수가 있다.

- inner 함수가 실행될 때 먼저 자체 변수 범위를 확인(이 떄 범위 내에서 정의된 y를 찾는다)

- 하지만 x에 대해 액세스 해야 하는 경우 범위 체인[Scope Chain]을 조회하여 찾는다.

- 이렇게 범위 체인을 사용하면 내부 함수가 외부 함수인 외부 범위에서 변수에 액세스 할 수 있다.

- 따라서 console.log(x + y)가 실행될 때 outer의 외부 범위에서 x와 자체 범위에서 y에 모두 액세스

- 여기서 범위 체인은 중첩된 범위에서 변수나 함수를 찾을 수 없을 경우 JS엔진은 전역 범위에 도달할 때까지 범위 체인에서 검색을 계속한다.

```렉시컬 환경```
- 스코프 체인은 실행컨텍스트의 렉시컬 환경을 단발향으로 연결한 것이다.
- 전역 렉시컬 환경은 코드가 로드되면 곧바로 생성되고 함수의 렉시컬 환경은 함수가 호출되면 곧바로 생성된다


```jsx
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
- 이처럼 꼬리를 물고 계속 범위를 넓히면서 찾는 관계를 스코프 체인 이라 한다.


4. 렉시컬 스코프

```jsx
var x = 1;

function foo () {
  var x = 10;
  bar ();
}

function bar() {
  console.log(x)
}

foo(); // 1
bar(); // 1
```

1. foo()를 호출하면 해당 범위 내에서 값이 10인 지역 변수 x를 선언한다.
2. foo() 내부에서 bar()함수를 호출한다.
3. bar() 함수에서 x를 기록할 때 함수 범위 내에서 변수 x를 찾는다.
4. bar 함수 내부에는 로컬 x가 선언되어 있지 않으므로 x라는 전역 변수를 찾는다.
5. foo()를 호출하면 아무것도 반환하지 않고 해당 범위 내에서 bar() 함수만 실행합니다.
6. bar() 함수 내에서 x 값을 기록합니다. bar() 함수에는 로컬 x가 없으므로 값이 1인 전역 변수 x를 찾습니다. 따라서 foo()를 호출하면 1이 기록됩니다.
7. foo()를 호출한 후 bar()를 직접 호출하면 x 값도 기록
8. bar() 함수에는 로컬 x가 없으므로 여전히 값이 1인 전역 변수 x를 찾습니다. 따라서 bar()를 호출하면 로그도 1이 됩니다

- JS는 렉시컬 스코프를 따르므로 함수를 어디서 호출했는지가 아니라 함수를 어디서 정의했는지에 따라 상위 스코프를 결정한다.

참고 : https://ljtaek2.tistory.com/145




















