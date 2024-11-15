# 네비게이션

- 상황에 맞게 화면 전환
- expo init react-native-navigation
- npm install --save @react-navigation/native --force
- import { createStackNavigator } from '@react-navigation/stack';

## 라이브러리 설치
- npx expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view -- --force
- npm install @react-navigation/stack --force

### 라이브러리 특징
- react-native-gesture-handler : 제스처 기반의 사용자 인터페이스를 만들 수 있도록 해주는 라이브러리로 기본적이 터치, 스와이프, 드레그를 인식하고 처리
- react-native-reanimated : 애니메이션을 구현, 기존 애니메이션 라이브러리보다 더 부드럽게 구현됨
- react-native-screens : 화면 이동과 관련된 자원을 효율적으로 관리해서 화면전환을 매끄럽게 해줌
- react-native-safe-area-context : 아이폰X이후 기기 상단에 노치나 인디케이터를 고려해 레이아웃을 안전하게 조정
- @react-native-community/masked-view : View에 마스크(mask)를 씌울 수 있도록 해줌, 네비게이션과 함께사용해 전환효과를 더 자연스럽게 만든다.

## 네비게이션 구조
- 리액트 네비게이션에는 NavigationContainer 컴포넌트, Navigator 컴포넌트, Screen 컴포넌트가 있다. (포함관계 : NavigationContainer 안에 Navigator 안에 Screen)

### Navigator 컴포넌트
- 계층구조 상태 관리하는 컨테이너 역할 (감싸는 역할, 포함하는 역할)

### Screen 컴포넌트 
- 화면으로 사용할 컴포넌트 지정
- name : 이 이름을 통해 다른 화면에서 해당 화면으로 네비게이션할 수 있다
- component : 이 속성에 지정된 컴포넌트가 화면에 렌더링된다
- Screen으로 에 해당되는 컴포넌트에는 navigation 과 route가 넘어간다.
- route.param 으로 받아 사용할 수 있다.

## 함수
- navigation.navigate("호출될이름",{키:값}) : 이벤트시 해당경로로 가도록 설정
- navigation.replace("호출될이름",{키:값}) : 되돌아가기 눌렀을때 대체되도록 설정




```js
<NavigationContainer>
    <Stack.Navigator>
        <Stack.Screen name="호출될이름1" component={이동할 컴포넌트1}/>
        <Stack.Screen name="호출될이름2" component={이동할 컴포넌트2}/>
    </Stack.Navigator>
</NavigationContainer>


const 컴포넌트 =({navigation, route})=>{
     return(
        //navigation.navigate('') 로 이동할 수 있다.
        ... onPress={()=> navigation.navigate('호출될이름2',{키1:값1, 키2:값2})} ----> route 로 전달된다.
     )
 }
```
### {키:값} 이동경로에서 받아쓰는 방법

```js
const 컴포넌트명 = ({ route }) => {
  // 전달된 데이터는 route.params 객체로 접근합니다.
  const { 키1, 키2 } = route.params;
}
```