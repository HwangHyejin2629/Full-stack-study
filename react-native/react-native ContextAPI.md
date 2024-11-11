# ContextAPI
- 데이터를 전역으로 관리하고 사용하는 기능
- Context : const 변수명 = createContext() : 새로운 Contect 생성
```js
import React, { createContext } from 'react';
const MyContext = createContext(null);
```
- Provider : 데이터를 제공하는 역할 value 속성으로 Context에 공유할 데이터 전달
```js
const MyProvider = ({ children }) => { //Provider로 감싸고 있는 자식컴포넌트
  const sharedValue = 'Hello, Context!';

  return (
    <MyContext.Provider value={sharedValue}>
      {children}
    </MyContext.Provider>
  );
};
```
- Consumer : Context에서 가져온 데이터를 소비하는 역할 Provider가 제공하는 데이터 직업 사용
- Consumer 컴포넌트의 자식은 컴포넌트를 반환하는 함수여야 하고, 이 함수는 Context의 현재값을 파라미터로 전달받아 데이터를 사용할 수 있다
- 가장 가까운 Provider 컴포넌트에서 값을 받으므로, 자식 컴포넌트 중 Provider 컴포넌트가 있다면 그 이후의 자식 컴포넌트 중간에 있는 Provider 컴포넌트가 전달하는 값을 사용
```js
const User = () => {
    return (
        <UserContext.Provider value={{name:'React Native'}}>
            <UserContext.Consumer>
                {value => <StyledText>Name: {value.name}</StyledText>}
            </UserContext.Consumer>
        </UserContext.Provider>      
    );
};
```