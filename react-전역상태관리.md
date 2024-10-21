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

- 
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

### 액션  action.js 만들기
- 액션 객체를 반환하는 함수 생성
-  타입(type)을 가진 객체 
- export const 함수명 = () => ({type:"액션타입명", ...})
```js
//action.js

export const addToCart = (id, name) => ({
    type: 'ADD_TO_CART',
    id,
    name,
  });
```

### 리듀서 함수 만들기
- 액션에 따라 상태를 변경하는 함수

#### 기본구조 
1. 현재상태 
2. 액션


### Provide 컴포넌트 : index.js 감싸기
- 애플리케이션 전체에 스토어 제공
- 최상위 컴포넌트를 감싸서 모든 자식 컴포넌트가 Redux 스토어에 접근 할 수 있게 해준다.

```js
//index.js

root.render(
  <Provider store={store}> 
    <ShopApp />
  </Provider>,
  document.getElementById('root')
);
```


