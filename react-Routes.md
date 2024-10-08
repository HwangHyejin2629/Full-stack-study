# 리액트 라우터

- 브라우저의 새로고침 없이 URL을 변경하고 해당 URL에 맞는 컴포넌트 렌더링하는 방법
- 페이지 전환 시 깜빡임 없애고, 뒤로가기 앞으로가기 (네비게이션 기능) 동작 원활하게 한다.

## 리액트 라우터 설치
- Terminal -> npm install react-router-dom

## index.js 수정

- BrowserRouter 을 import 한다.
- 보여줄 컴포넌트 <App />을 <BrowserRouter> 로 감싼다.

```js
import { BrowserRouter } from 'react-router-dom';

ReactDOM.render(
  <BrowserRouter> 
    <App />
  </BrowserRouter>,
  document.getElementById('root')
);
```

## App.js 수정
- Routes, Route 를 import 한다.
- return 안에 <Routes>, <Route> 코드 작성


