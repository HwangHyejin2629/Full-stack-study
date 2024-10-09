# 비동기처리

- 시간이 오래걸리는 작업이 완료되는 동안 UI가 반응하고 다른작업이 실행되도록 한다.

## 콜백함수(Callback function)
- 매개변수로 함수 객체를 전달해서 호출 함수 내에서 매개변수 함수를 실행하는 것
- 특정 작업이 완료된 후에 호출되는 함수이다.
- function fetchData(callback){ 값1; collback(값1);}
- fetchData(함수);
- callback(값1)  : 받은 함수를 가지고 값1을 적용하여 반환한다.

```js
function fetchData(callback) {
  setTimeout(() => {
    const data = '서버에서 받은 데이터';
    callback(data); // 작업이 끝난 후 콜백 실행
  }, 2000); // 2초 뒤에 실행
}

console.log('API 요청 시작');
fetchData((result) => {  //Callback에 함수자체를 집어넣는다.
  console.log('API 응답:', result);
});
console.log('다음 작업 진행');
```
fetchData 함수는 2초 후에 데이터를 반환하고, 데이터를 받은 후 콜백 함수가 실행된다.<br/>
그러나 2초를 기다리는 동안 다음 작업은 즉시 실행된다.

## Promise

- 비동기 작업 완료시 성공, 실패 반환하는 객체 : 비동기 처리시점 명확히 알수 있다.
- then 과 catch 로 성공 실패 처리
- resolve("값"): 작업이 성공한 경우 반환 값
- reject("값"): 작업이 실패한 경우 반환할 값
```js
const fetchData = () => {
    const promise = new Promise((resolve, reject) => { 
        if(...){
            resolve("성공!");  // 성공시 "성공!"을 반환한다
        } else{
            reject("실패!");   //실패시 "실패!" 를 반환한다.
        }
    });
}
fetchData()  //결과에 따라 then과 catch 블록이 실행됩니다.
  .then(data => { //then() : Promise가 성공(즉, resolve 호출)하면 실행되는 콜백 함수입니다. 콘솔에 응답 데이터('데이터 받아옴')를 출력합니다.
    console.log('API 응답:', data); 
  })
  .catch(error => {// Promise가 실패(즉, reject 호출)하면 실행되는 콜백 함수입니다. 여기서는 에러 메시지를 콘솔에 출력합니다.
    console.error('에러:', error);
  });
```

## async/await

- Promise 기반의 비동기 처리 방식
- 동기 처리같아 보이는 비동기 처리 수행
- await : 함수 앞에 붙으며, Promise가 해결될때까지 기다린다.
- async : 함수 앞에 붙으며, 비동기함수임을 나타낸다.<br/>
비동기함수는 항상 Promise 반환 <br/>
함수 내부에서 return값은 자동으로 resolve로 처리된다.
```js
async function fetchData() {
  return '데이터';
}

// fetchData()는 Promise를 반환함
fetchData().then(data => console.log(data)); // "데이터"
```