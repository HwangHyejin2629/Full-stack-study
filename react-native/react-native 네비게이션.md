# 네비게이션

- 상황에 맞게 화면 전환
- expo init react-native-navigation
- npm install --save @react-navigation/native --force
- import { createStackNavigator } from '@react-navigation/stack';

### 라이브러리 설치
- npx expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view -- --force
- npm install @react-navigation/stack --force

#### 라이브러리 특징
- react-native-gesture-handler : 제스처 기반의 사용자 인터페이스를 만들 수 있도록 해주는 라이브러리로 기본적이 터치, 스와이프, 드레그를 인식하고 처리
- react-native-reanimated : 애니메이션을 구현, 기존 애니메이션 라이브러리보다 더 부드럽게 구현됨
- react-native-screens : 화면 이동과 관련된 자원을 효율적으로 관리해서 화면전환을 매끄럽게 해줌
- react-native-safe-area-context : 아이폰X이후 기기 상단에 노치나 인디케이터를 고려해 레이아웃을 안전하게 조정
- @react-native-community/masked-view : View에 마스크(mask)를 씌울 수 있도록 해줌, 네비게이션과 함께사용해 전환효과를 더 자연스럽게 만든다.

## 네비게이션 구조
- 리액트 네비게이션에는 NavigationContainer 컴포넌트, Navigator 컴포넌트, Screen 컴포넌트가 있다. (포함관계 : NavigationContainer 안에 Navigator 안에 Screen)
- name : 이 이름을 통해 다른 화면에서 해당 화면으로 네비게이션할 수 있다
- component : 이 속성에 지정된 컴포넌트가 화면에 렌더링된다
- Screen으로 에 해당되는 컴포넌트에는 navigation 과 route가 넘어간다.
- route.param 으로 받아 사용할 수 있다.

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

## 스택 네비게이션
- 화면위에 화면을 쌓아 이동 : push 들어가기, pop 나가기
- stack 자료구조로 push으로 화면 쌓으며 이동, pop으로 이전화면으로 돌아가기 

### 설치
- npm install @react-navigation/stack --force
- npm install @react-navigation/stack@6.4.1 --force

## 작업순서
1. 화면을 구성할 컴포넌트 만든다
2. Navigation 만들고, Screen 컴포넌트 만든다
3. Screen 컴포넌트에 우리가 만든 화면 컴포넌트 할당
4. NavigationContainer 컴포넌트로 Navigation 컴포넌트 감싼다.

- initialRouteName 으로 처음 나올 화면 지정가능
```js
<Stack.Navigator initialRouteName="호출될이름1">
    <Stack.Screen name="호출될이름1" component={이동할 컴포넌트1}/>
    <Stack.Screen name="호출될이름2" component={이동할 컴포넌트2}/>
</Stack.Navigator>
```
## 스타일 주기
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

### useLayoutEffect
- 화면 그리기 전에 실행 : 화면이 보이기 전 UI를 수정할 수 있는 기회를 갖는다.
- 컴포넌트의 레이아웃을 읽어오고 설정할때, 화면 크기에 따라 UI 요소의 위치나 크기를 동적으로 조정해야 할때 사용
- 애니메이션 및 레이아웃 전환 : 특정 상태가 변하면 UI 레이아웃에서 애니메이션을 추가해야하는 경우
```js
const Item = ({ navigation, route }) => {

  useLayoutEffect(() => {

    navigation.setOptions({

      headerBackTitleVisible: false,
      headerTintColor: '#ffffff',
      headerLeft: ({ onPress, tintColor }) => {
        return (
          <MaterialCommunityIcons
            name="keyboard-backspace"
            size={30}
            style={{ marginLeft: 11 }}
            color={tintColor}
            onPress={onPress}
          />
        )}
      },
      headerRight: ({ tintColor }) => (
        <MaterialCommunityIcons
          name="home-variant"
          size={30}
          style={{ marginRight: 11 }}
          color={tintColor}
          onPress={() => navigation.popToTop()}
        />
      ),
      
    });

  }, [])

}
  ```

## 헤더 관리
- 헤더 이름 바꾸기 : options={headerTitle:""}
```js
    <Stack.Screen 
    name="List" 
    component={List}
    options={{headerTitle : 'List Screen'}} />
```
### 헤더 스타일 바꾸기 : screenOptions={{속성}}
```js
<Stack.Navigator 
    initialRouteName="Home"
    screenOptions={{
        cardStyle:{backgroundColor:'#ffffff'},
        headerStyle:{
            hegiht:110,
            backgroundColor:'#95a5a6',
            borderBottomWidth: 5,
            borderBottomColor : '#34495e',
        },
        headerTitleStyle : {color:'#ffffff', fontSize: 24},
    }}
>
```
- headerStyle : 헤더의 배경색 수정
- headerTitleStyle : 헤더와 타이틀 컴포넌트의 스타일을 수정
- headerTitleStyle을 이용해 타이틀의 스타일을 변경
- headerBackTitleVisible : 뒤로가기 버튼의 글씨를 표시 true,false
- headerBackTitle :  뒤로가기 버튼의 내용 설정
- headerTintColor :  뒤로가기 버튼이나 헤더 텍스트의 색상을 설정

### 헤더 감추기
#### headerMode
- Navigator 의 컴포넌트 속성으로 헤더를 렌더링하는 방법 설정
- 속성값
<br/>float : 헤더가 상단에 유지되며 하나의 헤더를 사용 (ios), 화면 전환시 부드럽다
<br/>screen : 각 화면마다 헤더를 가지며 화면 변경과 함께 나타나거나 사라진다. (Android)
<br/>none : 헤더가 렌더링 되지 않는다. (=false) 모든화면에서 헤더가 사라진다.

#### headerShown
- 화면옵션으로 Navigator 컴포넌트의 screenOptions에 설정하여 전체 화면의 헤더가 보이지 않게 설정
```js
<Stack.Screen name="Home" component={Home} options={{headerShown:false}}/>

```

## 탭 네비게이션
- npm install @react-navigation/bottom-tabs@6.5.20 --force
- import { createBottomTabNavigator } from "@react-navigation/bottom-tabs";



