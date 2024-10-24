# Redux 전역상태 관리
## 기본 개념
- Redux : 상태 관리 라이브러리, 여러 컴포넌트들의 상태공유를 중앙 집중화된 스토어로 관리

- 스토어(Store) : 애플리케이션 전역상태 저장하는 곳
<br/>createStore() 함수 사용하여 생성

- 액션(Action) : 상태 변경을 위해 발생시키는 이벤트
<br/> { type: 'ACTION_TYPE', payload: 데이터 }

- 디스패치(Dispatch) : 액션을 스토어에 전달하는 메서드

- 리듀서(Reducer) : 상태를 변경하는 순수함수
<br/> 순수함수 : 주어진 입력만을 사용해서 결과 도출, 함수 외부의 상태나 변수에 의존하지 않는다. 동일한 입력값에 동일한 결과 반환

```js
function add(a, b) {
  return a + b;
}

add(2, 3); // 항상 5를 반환
// 함수는 함수 내부의 로컬 변수와 입력 값만 사용하며, 외부의 변수나 상태를 변경하거나 의존하지 않는다.
```
```js
multiply(5); // 외부 값인 externalValue와는 무관하게 작동

//함수가 외부의 상태나 변수에 영향을 주지 않으며, 입력 값만 처리하고 반환한다.

let count = 0;

function increaseCount() {
  count++; // 전역 상태를 변경하는 부작용이 발생함 -> 순수 함수가 아님
}
```


## 동작 원리

1. 스토어 생성 : 애플리케이션 상태를 보관
2. 액션 디스패치 : 사용자 인터랙션이나 기타 이벤트에 따라 액션을 디스패치
3. 리듀서 호출 : 디스패치된 액션을 리듀서가 받아 새로운 상태 계산
4. 상태 업데이트 : 스토어의 상태가 업데이트되고, 구독되는 컴포넌트 리렌더링

## 작업 순서

### Redux 바인딩 라이브러리 설치 
- npm install redux react-redux
- 바인딩 라이브러리 : 두 개 이상의 시스템이나 라이브러리 간의 연결을 원활하게 해주는 역할을 한다.

### 액션 함수 action.js 만들기
- 액션 객체를 반환하는 함수 생성
-  타입(type)을 가진 객체 
- export const 함수명 = () => ({type:"액션타입명", ...})
```js
//action.js

export const increment = () => ({
  type: 'INCREMENT', // 액션의 타입을 'INCREMENT'로 정의. 
  // 이 액션은 리듀서에서 상태를 증가시키기 위한 신호로 사용됨
});

// 'DECREMENT'라는 타입의 액션을 반환하는 함수
export const decrement = () => ({
  type: 'DECREMENT', // 액션의 타입을 'DECREMENT'로 정의. 
  // 이 액션은 리듀서에서 상태를 감소시키기 위한 신호로 사용됨
});

```

### 리듀서 함수 reducer.js 만들기 
- 액션에 따라 상태를 변경하는 순수함수
- 상태를 직접 변경하지 않고, 새로운 객체를 반환하여 "불변성" 유지

#### 기본구조 
1. 현재상태(state)
  - 리듀서가 관리하는 현재 상태, 처음 호출될때 초기 상태

```js
// 초기 상태(initialState)를 정의함. count는 0으로 초기화됨.
const initialState = {
  count: 0,
};
```  
2. 액션(action)
  - 상태를 변경할 이벤트 : 액션 객체의 상태를 어떻게 변경할지 알려줌
  - 현재상태와 액션객체를 인자로 받아 새로운 상태 반환
  - ...state : 초기상태를 얕게 복사한다. (불변성)
  - switch문 사용 : type마다 다른 결과값 도출시킴

```js
// state가 undefined일 경우, initialState를 기본 값으로 사용함.
const counterReducer = (state = initialState, action) => {

  // 액션의 타입에 따라 상태를 변경하기 위한 switch문을 사용함.
  switch (action.type) {
    // 'INCREMENT' 액션일 경우, count 값을 1 증가시킨 새로운 상태를 반환함.
    case 'INCREMENT':
      return {
        ...state, // 기존 상태를 복사하고
        count: state.count + 1, // count 값을 1 증가시킴
      };
    
    // 'DECREMENT' 액션일 경우, count 값을 1 감소시킨 새로운 상태를 반환함.
    case 'DECREMENT':
      return {
        ...state, // 기존 상태를 복사하고
        count: state.count - 1, // count 값을 1 감소시킴
      };
    
    // 액션 타입이 매치되지 않을 경우, 현재 상태를 그대로 반환함.
    default:
      return state; // 상태 변경 없이 현재 상태를 반환함
  }
};

export default counterReducer;
```

### 스토어(store) 객체 store.js 만들기
- 애플리케이션 상태 저장하는 객체
- createStore 함수 불러오기 : import {createStore} from 'redux';
- 리듀서(reducer) 불러오기 : import 리듀서함수명 from '리듀서js경로';
- 스토어 생성 : const store = createStore(리듀서함수명)

```js
import { createStore } from 'redux';

// 리듀서(reducer)를 import 함. 
// 이 리듀서는 애플리케이션의 상태 변경 로직을 정의한 함수임
import counterReducer from './reducer';

// counterReducer를 스토어에 인자로 전달하여 상태 변경 로직을 정의한다.
// 스토어는 애플리케이션 전체의 상태를 관리하고, 
// 액션이 발생하면 리듀서를 통해 상태를 업데이트함
const store = createStore(counterReducer);

export default store;

```
### Redux 와 React 연결하기
- redux 함수 가져오기 : import { Provider, useDispatch, useSelector } from 'react-redux'; 
- 스토어 함수 가져오기 : import 스토어함수이름 from '스토어 경로'; 
- 액션함수 가져오기 : import { 액션함수1,액션함수2 } from '액션함수경로';
- useSelector() : Redux 스토어에서 상태를 읽어오는 Hook
- useDispatch() : Redux 스토어에 액션을 보낼 수 있는 Hook
  <br/>이 Hook을 사용해 액션을 디스패치할 수 있음
- dispatch(액션함수명()) : 사용자 입력에 따른 액션 디스패치

```js
// App.js

import React from 'react';
import { Provider, useDispatch, useSelector } from 'react-redux'; 
import store from './store'; 
import { increment, decrement } from './actions'; 

function Counter() {
  // 스토어의 상태 중 count 값을 선택해서 가져옴
  const count = useSelector((state) => state.count);
  
  // useDispatch: Redux 스토어에 액션을 보낼 수 있는 Hook
  // 이 Hook을 사용해 액션을 디스패치할 수 있음
  const dispatch = useDispatch();

  return (
    <div>
      {/* 현재 상태인 count 값을 화면에 출력함 */}
      <h1>Counter: {count}</h1>
      
      {/* Increment 버튼을 클릭하면 increment 액션을 디스패치함 */}
      <button onClick={() => dispatch(increment())}>Increment</button>

      {/* Decrement 버튼을 클릭하면 decrement 액션을 디스패치함 */}
      <button onClick={() => dispatch(decrement())}>Decrement</button>
    </div>
  );
}
```

### Provide 컴포넌트로 감싸기
- 애플리케이션 전체에 스토어 제공
- 최상위 컴포넌트를 감싸서 모든 자식 컴포넌트가 Redux 스토어에 접근 할 수 있게 해준다.

```js
//App.js

function App() {
  return (
    {/* Provider 안에 있는 모든 컴포넌트는 Redux 스토어에 접근할 수 있음 */}
    <Provider store={store}> 
    {/* Counter 컴포넌트는 Redux 스토어에서 상태를 읽고, 액션을 디스패치할 수 있음 */}
      <Counter />   
    </Provider>
  );
}

export default App; 
```

## 실행 흐름

1. 컴포넌트 랜더링 및 상태 표시
  - 처음 렌더링할때 userSelecter() 훅으로 현재 상태를 읽어온다.

2. 사용자 입력에 따른 액션 디스패치
  - 이벤트시 해당 dispatch()로 액션함수 실행
```js
<button onClick={() => dispatch(increment())}>Increment</button>
```
3. 리듀서 액션 처리

4. 상태 업데이트 및 컴포넌트 리렌더링
  - 상태 변경되면 useSelector()로 리렌더링
