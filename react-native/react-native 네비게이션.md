# 네비게이션

- 상황에 맞게 화면 전환
- expo init react-native-navigation
- npm install --save @react-navigation/native --force


### 라이브러리
- 리엑트네이비게이션은 기능별 분리된 모듈로 되있어 개별적으로 라이브러리 설치해야한다.
- 라이브러리 설치 : npx expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view -- --force
- npm install @react-navigation/stack --force

- react-native-gesture-handler : 제스처 기반의 사용자 인터페이스를 만들 수 있도록 해주는 라이브러리로 기본적이 터치, 스와이프, 드레그를 인식하고 처리
- react-native-reanimated : 애니메이션을 구현, 기존 애니메이션 라이브러리보다 더 부드럽게 구현됨
- react-native-screens : 화면 이동과 관련된 자원을 효율적으로 관리해서 화면전환을 매끄럽게 해줌
- react-native-safe-area-context : 아이폰X이후 기기 상단에 노치나 인디케이터를 고려해 레이아웃을 안전하게 조정
- @react-native-community/masked-view : View에 마스크(mask)를 씌울 수 있도록 해줌, 네비게이션과 함께사용해 전환효과를 더 자연스럽게 만든다.

## 스택 네비게이션
- npm install @react-navigation/stack --force
- npm install @react-navigation/stack@6.4.1 --force
- 화면위에 화면을 쌓아 이동
- stack 자료구조로 push으로 화면 쌓으며 이동, pop으로 이전화면으로 돌아가기 

## 네비게이션 작업 흐름
1. NavigationContainer로 StackNavigation을 자식으로 갖는다(감싼다)
2. StackNavigator로 Stack.screen 컴포넌트를 자식으로 갖는다 
3. 각각 Screen 컴포넌트는 navigation과 route를 props로 받는다
4. navigation을 통하여 설정을 줄 수 있고, 다른 화면으로 이동이 가능하다.
5. route.param을 통해 전달받은 데이터를 사용할 수 있다. 



## 헤더감추기
- headerMode : Navigator 의 컴포넌트 속성으로 헤더를 렌더링하는 방법 설정
- headerShown : 화면옵션으로 Navigator 컴포넌트의 screenOptions에 설정하여 전체 화면의 헤더가 보이지 않게 설정

- 속성값
<br/>float : 헤더가 상단에 유지되며 하나의 헤더를 사용 (ios)
<br/>screen : 각 화면마다 헤더를 가지며 화면 변경과 함께 나타나거나 사라진다. (Android)
<br/>none : 헤더가 렌더링 되지 않는다. (=false)



