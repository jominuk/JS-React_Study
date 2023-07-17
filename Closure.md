# Closure(클로저)

- 내부 함수에서 상위 함수 스코프의 변수에 접근할 수 있는 개념
- react에서 함수형 컴포넌트의 상태 관리를 위해 컴포넌트 외부에 저장된 값을 사용하며, 클로저를 통해 해당 값에 접근해 상태를 비교하고 변경
- 클로저는 주변 상태(렉시컬 환경)을 기억하여 외부 범위에서도 접근이 가능한 것을 얘기함

- 이러한 개념은 이벤트 핸들러로 작업할 때 React에서 자주 사용된다.

```javascript
function Button() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return <button onClick={handleClick}>Click me ({count})</button>;
}
```

1. 이 구성요소가 렌더링 되면 handleClick 함수가 생성되고 정의된다.
2. 클로저 덕분에 둘러싸는 범위에서 개수 상태 변수를 액세스 할 수 있다.
3. 버튼을 클릭하면 handleClick 함수는 구성 요소가 다른 count값으로 다시 렌더링 되더라도 생성 당시의 count값을 기억한다.

- 이는 handleClick 함수가 count 변수에 클로저를 형성했기 때문

4. handleClick 호출되면 클로저에서 캡처한 값을 사용하여 카운트를 1씩 증가
5. setCount 함수는 상태를 업데이트하여 구성요소의 다시 렌더링을 트리거하고 업데이트된 count 값을 표시

- Button이 렌더링되면 count 변수에 대한 참조를 포함하는 자체 클로저와 함께 handleClick 함수의 새 인스턴스가 생성됩니다.
- 버튼을 클릭하면 handleClick 함수가 호출되고 setCount 함수를 사용하여 카운트 상태를 업데이트합니다.

- 클로저는 React에서 중요한 개념이다.
  - 클로저는 함수가 실행을 마친 후에도 어휘 환경의 값을 `기억`할 수 있도록 하는 강력한 개념

```javascript
import React, { useEffect, useState } from "react";

const ClosureInReact = () => {
  const [count, setCount] = useState(1);

  const incrementCount = () => {
    // closure
    setCount(count + 1);
  };

  useEffect(() => {
    const timer = setTimeout(() => {
      incrementCount();
    }, 1000);

    return () => {
      clearTimeout(timer);
    };
  }, [incrementCount]);

  return <div>{`Timer started: ${count}`}</div>;
};

export default ClosureInReact;

// 매초마다 증가하는 타이머를 작성하였다.
```

## 클로저의 활용

### - 상태를 안전하게 변경하고 유지하기 위해 사용

```javascript
// 카운트 상태 변경 함수
const increase = (function () {
  // 카운트 상태 변수
  let num = 0;
  // 클로저
  return function () {
    // 카운트 상태를 1만큼 증가시킨다.
    return ++num;
  };
})();
console.log(increase()); // 1
console.log(increase()); // 2
console.log(increase()); // 3
```
