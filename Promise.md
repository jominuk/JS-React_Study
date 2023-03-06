# Promise

- 비동기적인 작업을 수행할 때 사용하는 JS 객체
  - 비동기처리 : 특정 코드의 실행이 완료될 때까지 기다리지 않고 다음 코드를 먼저 수행하는 JS 특성을 의미

## Promise의 상태

1. Pending(대기) : Promise 객체를 생성된 상태아며, 아직 작업이 수행되지 않은 상태

```javascript
new Promise((resolve, reject) => {});
```

2. Fullfilled(이행) : 작업이 성공적으로 수행된 상태, 이 때 작업 결과 값을 가지고 있음

```javascript
new Promise(function (resolve, reject) {
  resolve();
});

// 이행 상태가 되면 then()을 활용하여 결과값을 받을 수 있음
function getData() {
  return new Promise((resolve, reject) => {
    let data = 10;
    resolve(data);
  });
}

getData().then((resolvedData) => console.log(resolvedData));

//10
```

3. Rejected(실패) : 작업이 실패한 상태, 이 때 실패 이유를 가지고 있음

```javascript
new Promise(function (resolve, reject) {
  reject();
});

// resolve와 마찬가지로, 실패 상태가 되면 catch()를 활용하여 결과값을 받고 예외 처리할 수 있음

function getData() {
  return new Promise((resolve, reject) => {
    reject(new Error("This is rejected!"));
  });
}

getData().catch((err) => console.log(err));
```

## then(), catch()

- then()은 작업이 성공적으로 완료되었을 때 호출, catch()는 작업이 실패하였을 때 호출

```javascript
promise
  .then((result) => {
    // 작업이 성공적으로 완료되었을 때 처리할 작업
  })
  .catch((error) => {
    // 작업이 실패하였을 때 처리할 작업
  });
```
