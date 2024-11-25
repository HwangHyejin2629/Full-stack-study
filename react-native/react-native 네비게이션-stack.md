# 스택 네비게이션
- 화면위에 화면을 쌓아 이동 : push 들어가기, pop 나가기
- stack 자료구조로 push으로 화면 쌓으며 이동, pop으로 이전화면으로 돌아가기 

## 설치
- npm install @react-navigation/stack --force
- npm install @react-navigation/stack@6.4.1 --force

## 작업순서
1. 화면을 구성할 컴포넌트 만든다
2. Navigation 만들고, Screen 컴포넌트 만든다
3. Screen 컴포넌트에 우리가 만든 화면 컴포넌트 할당
4. NavigationContainer 컴포넌트로 Navigation 컴포넌트 감싼다.

- initialRouteName 으로 처음 나올 화면 지정가능
```js
import { createStackNavigator } from '@react-navigation/stack';

const Stack = createStackNavigator();

<Stack.Navigator initialRouteName="호출될이름1">
    <Stack.Screen name="호출될이름1" component={이동할 컴포넌트1}/> 
    {/*이동할컴포넌트에 </> 안씀 */}
    <Stack.Screen name="호출될이름2" component={이동할 컴포넌트2}/>
</Stack.Navigator>
```

## 설정의 우선순위
- 작은 범위 설정일수록 우선순위가 높다

### 스타일 주기
- Navigation 에 스타일주기 : 하위 스크린에 다 적용
```js
<Stack.Navigator 
    initialRouteName="호출될이름1"
    screenOption={{옵션}}
>
```
- Screen 컴포넌트에 스타일 주기 : 해당 스크린만 적용
```js
<Stack.Screen 
    name="호출될이름1" 
    component={이동할 컴포넌트1}
    options={{옵션}}
/>
```
- 화면으로 사용되는 컴포넌트에서 navigation 객체를 사용해 스타일 주기 : 해당 스크린만 적용
```js
const Item ({navigation})=>{
    navigation.setOption({옵션})
}
```



