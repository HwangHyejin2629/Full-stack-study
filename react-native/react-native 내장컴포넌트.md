# 냐장컴포넌트
## App

- <App /> : src 폴더를 만들어서 App.js 를 만들어 내용을 표현하고, root 에 있는 App.js 에 연결하여 화면으로 보여준다.
```js
import App from './src/App';

export default App;
```

## View Fragment
- <View> </View> : <div> 와 비슷한 역할을 한다 태그들을 하나로 감싸서 에러 방지
- <Fragment> </Fragment>, <> </>  : <View> 대신 사용가능하며, key속성을 사용하여 리스트 렌더링시 유용
- <Text> 글 내용 </Text> : 글을 쓸때 글 담는 태그

```js
export default function App() {
  return (
    <View style={styles.container}>
      <Text>Open up App.js to start working on your app!</Text>
      <StatusBar style="auto" />
    </View>
  );
}
```
## Text
- <Text></Text> : 텍스트를 표시할때 사용 <p>,<span>과 비슷한 역할

## Button
- 사용법 : https://reactnative.dev/docs/button 
- title : 버튼 내부에 출력되는 텍스트
- onPress : 버튼 눌렸을때 호출 되는 함수 지정
- 안드로이드와 ios 의 Button 의 color 속성 적용이 다르다.
```js
<Button title="button" onPress={()=> alert('Click!!')}/>
```
## ScrollView
- 스크롤 가능한 뷰 만들때 사용
```js
import React from 'react';
import { ScrollView, View, Text, StyleSheet } from 'react-native';

export default function App() {
  return (
    <ScrollView style={styles.container}>
      {Array.from({ length: 20 }, (_, i) => (
        <View key={i} style={styles.item}>
          <Text>Item {i + 1}</Text>
        </View>
      ))}
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f5f5f5',
  },
  item: {
    padding: 20,
    borderBottomWidth: 1,
    borderBottomColor: '#ccc',
    alignItems: 'center',
  },
});

```
## TextInput
- 입력칸 만드는 컴포넌트
```js
<TextInput
  onChangeText={onChangeText}
  value={text}
  placeholder="입력하세요"
  style={styles.input}
/>
```

## Pressable 
- 터치 이벤트에 세부적인 제어를 제공
- onPress: 사용자가 컴포넌트를 눌렀다 떼었을 때 호출된다.
- onPressIn: 사용자가 컴포넌트를 누르는 순간 호출된다.
- onPressOut: 사용자가 눌렀다 뗄 때 호출된다.
- onLongPress: 사용자가 지정된 시간 이상 길게 눌렀을 때 호출된다. 길게 누르는 경우에만 특정 동작을 처리하고 싶을 때 유용하다.
- delayLongPress : 요소를 길게 누를 때 반응하는 데 필요한 지연 시간을 밀리초 단위 설정 
- hitSlop : 터치 영역을 확장 (픽셀단위)
- pressRetentionOffset : 사용자가 버튼을 누르고 있을 때, 손가락을 살짝 이동했을 때 버튼의 눌림 상태를 유지할 수 있는 영역 (픽셀단위)
```js
import React from 'react';
import {View, Text, Pressable} from 'react-native';

const Button = props => {
  return (
    <Pressable
      style={{padding: 10, backgroundColor: '#2598eb'}}
      onPressIn={() => {
        console.log('Press In');
      }}
      onPressOut={() => {
        console.log('Press Out');
      }}
      onPress={() => {
        console.log('Press');
      }}
      onLongPress={() => {
        console.log('Long Press');
      }}
      delayLongPress={3000}
      pressRetentionOffset={{button: 50, left: 50, right: 50, top: 50}}
      hitSlop={50}>
      <Text style={{padding: 10, fontSize: 30}}>{props.title}</Text>
    </Pressable>
  );
};

const App = () => {
  return (
    <View
      style={{
        flex: 1,
        justifyContent: 'center',
        backgroundColor: '#fff',
        alignItems: 'center',
      }}>
      <Button title="Pressable"></Button>
    </View>
  );
};
export default App;

```

## FlatList
- 데이터 목록을 간편하게 렌더링
- 배열형태의 데이터를 받아 각 항목을 화면에 표시
- data : 리스트에 표시할 데이터 배열
- renderItem: 각 아이템을 어떻게 렌더링할지 정의하는 함수
- keyExtractor : 각 아이템의 고유한 키 값을 지정하는 속성

## Image

- source : 이미지 경로지정
- style : 스타일 지정

```js
<Image source={{uri:'경로'}} style={styles.image}/>
```

### 이미지 원형으로 만들기
```js
const StyledImage=styled.Image`
    background-color:${({theme})=>theme.imageBackground};
    width:100px;
    height:100px;
    border-radius:${({rounded})=>{rounded?50:0}}px;
`

const Image = ({url, imageStyle}) => {
    return(
        <Container>
            <StyledImage source={{uri:url}} style={imageStyle} rounded={rounded}/>
        </Container>
    )
}
```

## ScrollView
- 모든 데이터를 한번에 렌더링하므로 렌더링해야 하는 데이터양을 알고 있을때 사용하는게 좋다.
- 렌더링할 데이터가 많을경우 렌더링 속도가 느려지고, 메모리 사용량 증가 등 성능이 저하된다.

## FlatList
- 화면에 적절한 데이터만 렌더링하고, 스크롤 이동에 맞춰 필요한 만큼 추가 렌더링
- 데이터 길이가 가변적이고 양을 예측할 수 없는 상황에 사용하기 좋다.
### 속성
1. 랜더링할 항목의 데이터를 배열로 전달
2. 전달된 배열의 항목을 이용해 항목을 렌더링하는 함수
3. 각 항목에 키를 추가하기 위해 고유한 값을 반환하는 함수