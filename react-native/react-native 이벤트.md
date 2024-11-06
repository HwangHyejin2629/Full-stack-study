# 이벤트 

## press이벤트
- onPress: 사용자가 컴포넌트를 눌렀다 떼었을 때 호출된다.
- onPressIn: 사용자가 컴포넌트를 누르는 순간 호출된다.
- onPressOut: 사용자가 눌렀다 뗄 때 호출된다.
- onLongPress: 사용자가 지정된 시간 이상 길게 눌렀을 때 호출된다. 길게 누르는 경우에만 특정 동작을 처리하고 싶을 때 유용하다.
- delayLongPress: onLongPress 가 호출되는 시간 조절
- onPressIn -> onPressOut -> onPress 혹은 onPressIn -> onLongPress -> onPressOut 순서로 호출된다.

## change이벤트
- <TextInput> 컴포넌트에서 많이 사용된다.
- onChange : 입력된 텍스트가 변경될때 호출
- 호출된 함수에 (event) => event.nativeEvent.text 로 인자를 받을 수 있다.