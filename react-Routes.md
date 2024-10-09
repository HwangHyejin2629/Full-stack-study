# 리액트 라우터

- 브라우저의 새로고침 없이 URL을 변경하고 해당 URL에 맞는 컴포넌트 렌더링하는 방법
- 페이지 전환 시 깜빡임 없애고, 뒤로가기 앞으로가기 (네비게이션 기능) 동작 원활하게 한다.

## 리액트 라우터 설치
- Terminal -> npm install react-router-dom

## index.js 수정

- BrowserRouter 을 import 한다.
- 보여줄 컴포넌트 <App />을 <BrowserRouter> 로 감싼다.

```js
import React from 'react';
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
- path ="/주소1"  element={<컴포넌트1 />}  URL을 주소1로 치고 들어가면 컴포넌트1를 렌더링한다.

```js
import React from 'react';
import { Routes, Route } from 'react-router-dom';
import Home from './Home';
import About from './About';

function App() {
  return (
    <div>
      <Routes>
        <Route path="/home" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </div>
  );
}
```

## Navbar.js 구성

- Link 를 import 한다.
- <nav> 안에 <Link> 구성
- <Link> 는 URL 변경하지 않고 페이지 간에 이동할 수 있는 링크를 만든다. 
- <Link to ="/경로">문자</Link>

```js
import React from 'react';
import { Link } from 'react-router-dom';

function Navbar() {
  return (
    <nav>
      <Link to="/home">홈</Link>
      <br/>
      <Link to="/about">소개</Link>
    </nav>
  );
}

export default Navbar;
```
- to 속성 : 이동할 경로 지정, 문자열과 객체 전달 가능
- state : 링크를 통해 전달할 추가 상태 정보를 담는다.

```js
<Link
  to={{ //객체 전달가능
    pathname: '/profile',  //이동경로
    state: { fromDashboard: true }, // 상태정보
  }}
>
  프로필
</Link>
```

## 동적라우트

- <Route> 의 path 속성에 콜론(:) 으로 파라미터 정의
- <Route path="/주소1/:파라미터" element={<이동페이지/>}>
- 이동페이지에서 useParams import 하고, useParams로 URL 파라미터에 접근할 수 있다. 
- const {파라미터}=useParams(); 
- URL의 파라미터의 키,값 의 객체를 반환 여러개일땐 {파라미터1,파라미터2} 이렇게 받는다.

```js
import React from 'react';
import { useParams } from 'react-router-dom';

function UserProfile() {
  const { id } = useParams(); 

  // 실제로는 id를 사용하여 서버에서 데이터를 가져온다
  const user = {
    id,
    name: id === '1' ? '홍길동' : id === '2' ? '이순신' : '김유신', //삼항연산자 -> id에 따라 다르게 결과 도출
    age: id === '1' ? 30 : id === '2' ? 45 : 38, 
  };

  return (
    <div>
      <h2>{user.name}님의 프로필</h2>
      <p>사용자 ID: {user.id}</p>
      <p>나이: {user.age}</p>
    </div>
  );
}

export default UserProfile;
```
## map() 함수
- 배열안의 내용을 반복해주는 함수 : 배열.map(현재요소 => { 로직 })

```js
import React from 'react';
import { Link } from 'react-router-dom';

function Categories() {
  const categories = [
    { id: 1, name: '전자제품' },
    { id: 2, name: '의류' },
    { id: 3, name: '식료품' },
  ];

  return (
    <div>
      <h1>카테고리 목록</h1>
      <ul>
        {categories.map(category => (  //<Link>를 배열에 맞게 생성하는 로직
          <li key={category.id}>
            <Link to={`/categories/${category.id}`}>{category.name}</Link> 
          </li>
        ))}
      </ul>
    </div>
  );
}

export default Categories;
```

## 리다이렉션

- 특정 조건에 따라 다른 페이지로 자동 이동 시키는 기능
- Navigate 컴포넌트 : 특정경로로 리다이렉트 하기위해 사용된다.
- Navigate를 import 해야한다.
- to : 이동시키려는 경로 
- replace={true} : 뒤로가기 안되도록 함, 기본값은 false

App.js
```js
import React from 'react';
import { Routes, Route } from 'react-router-dom';
import Home from './Home';
import NotFound from './NotFound';

function App() {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="*" element={<NotFound />} />  {/* 모든 경로는 NotFound로 이동해라 */}
    </Routes>
  );
}

export default App;
```

NotFound.js
```js
import React from 'react';
import { Navigate } from 'react-router-dom';

function NotFound() {
  // 사용자를 홈 페이지로 리다이렉트
  return <Navigate to="/" />;
}

export default NotFound;
```