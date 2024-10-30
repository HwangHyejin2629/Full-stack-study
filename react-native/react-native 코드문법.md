# 문법

## 기본 틀 만들때 사용되는 컴포넌트

- <App /> : src 폴더를 만들어서 App.js 를 만들어 내용을 표현하고, root 에 있는 App.js 에 연결하여 화면으로 보여준다.
```js
import App from './src/App';

export default App;
```
- <View> </View>, <Fragment> </Fragment>, <> </>  : 태그들을 하나로 감싸서 에러 방지
- <Text> 글 내용 </Text> : 글을 쓸때 글 담는 태그

## Props

- 해당 함수에서 매개변수 할당하기
- 보낼때 : <Com title=보낼내용1 value=보낼내용2/>보낼내용3</Com>
- 받을때 : const Com=(props)=>{ console("출력내용 : ",props.title, props.value, props.children) } 
<br>  --> 출력내용 : 보낼내용1보낼내용2보낼내용3

## useState

- import {useState} from 'react'
- const [item, setItem]=useState(0)

## 이벤트

- onChange : 상태가 변화할때 사용 event => event.nativeEvent.text로 텍스트 가져온다.
- onChangeText : text => text 로 가져온다.