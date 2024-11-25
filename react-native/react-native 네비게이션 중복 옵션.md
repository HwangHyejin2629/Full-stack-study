# 네비게이션 중복 옵션
- Navigator 에서 옵션 바꾸기 : screenOptions={{속성}}  
<br/>Navigator 내의 Screen 모든 속성을 변경할 수 있다.

- Screen 에서 옵션 바꾸기 : option={{속성}}
<br/> Screen의 속성을 변경할 수 있다.

- 기본화면 설정 : ninitialRouteName="기본화면네임"


## 헤더 옵션 바꾸기

### 헤더 이름 바꾸기
- headerTitle:"헤더이름"
```js
    <Stack.Screen 
    name="List" 
    component={List}
    options={{headerTitle : 'List Screen'}} />
```

### 헤더 스타일 바꾸기 
- headerStyle : 헤더의 배경색 수정
- headerTitleStyle : 헤더와 타이틀 컴포넌트의 스타일을 수정
- headerTitleStyle을 이용해 타이틀의 스타일을 변경
- headerBackTitleVisible : 뒤로가기 버튼의 글씨를 표시 true,false
- headerBackTitle :  뒤로가기 버튼의 내용 설정
- headerTintColor :  뒤로가기 버튼이나 헤더 텍스트의 색상을 설정
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

### 헤더 감추기
#### headerMode 
- Navigator 의 컴포넌트 속성으로 헤더를 렌더링하는 방법 설정
- 속성값
<br/>float : 헤더가 상단에 유지되며 하나의 헤더를 사용 (ios), 화면 전환시 부드럽다
<br/>screen : 각 화면마다 헤더를 가지며 화면 변경과 함께 나타나거나 사라진다. (Android)
<br/>none : 헤더가 렌더링 되지 않는다. (=false) 모든화면에서 헤더가 사라진다.

#### headerShown
- Screen 에서 사용
- 화면옵션으로 Navigator 컴포넌트의 screenOptions에 설정하여 전체 화면의 헤더가 보이지 않게 설정
- true, false 값을 가진다.
```js
<Stack.Screen name="Home" component={Home} options={{headerShown:false}}/>

```

### 헤더 돌아가기 버튼 없애기
- headerBackTitleVisible:false

## 헤더 버튼만들기
```js 
<Stack.Screan option={{headerRight:()=>(<Pressable><아이콘컴포넌트/></Pressable>)}}
```
