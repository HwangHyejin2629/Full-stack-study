# 스타일링

- expo init react-native-style

## 인라인 스타일링
- 컴포넌트에 직접 스타일 입력하는 방식
```js
<View
      style={{
        flex: 1,
        backgroundColor: '#fff',
        alignItems: 'center',
        justifyContent: 'center',
      }}
> 
    <Text>내용</Text> 
</View>
```

## 클래스 스타일링
- 스타일시트에 정의된 스타일을 사용하는 방법
- StyleSheet : React Native의 내장 객체로, 화면에 표시될 요소들의 디자인(예: 배경색, 글꼴 크기, 여백)을 지정하는 역할을 한다.
- const 스타일명 = StyleSheet.create({키1 : { 스타일속성 }, 키2 : { 스타일속성}})
- <컴포넌트명 style={{스타일명.키1}}>
```js
<View style={styles.container}>
      <Text style={styles.text}>
        Inline Styling - Text
      </Text>
      <Text style={styles.error}>Inline Styling - Error</Text>
</View>
...
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
  text: {
    padding: 10,
    fontSize: 26,
    fontWeight: '600',
    color: 'black',
  },
  error: {
   padding: 10,
    fontSize: 26,
    fontWeight: '400',
    color: 'red',
  },
});

```

## 주요 스타일 속성