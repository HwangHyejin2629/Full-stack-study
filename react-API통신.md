# API 통신하기

## Fetch API

- react에서 기본 제공
- 데이터 받아서 JSON 으로 변환하는 과정 필요
- fetch('주소').then(data=>data.json()).catch(error=>에러 처리)
```js
// Fetch API 사용 예시
fetch('https://jsonplaceholder.typicode.com/posts')
  .then(response => response.json()) // JSON 형식으로 응답을 변환
  .then(data => console.log(data))   // 데이터 출력
  .catch(error => console.error('Error:', error)); // 에러 처리
```

## Axios

- axios 설치 후 사용 가능, 자동 JSON 변환
- npm install axios
- axios.get('주소').then(data => 처리 방법).catch(error=> 에러 처리)
```js
import axios from 'axios';

axios.get('https://jsonplaceholder.typicode.com/posts')
  .then(response => console.log(response.data))  // 데이터 출력
  .catch(error => console.error('Error:', error)); // 에러 처리
```


