# Drawer 네비게이션

- Drawer : 서랍
- 버튼 누르면 메뉴가 나오는 형태
- npm install @react-navigation/drawer@6.7.2 --force
```js
import React from "react";
import { createDrawerNavigator } from '@react-navigation/drawer';

const Drawer = createDrawerNavigator();

const DrawerkNavigation = () => {

    return(
        <Drawer.Navigator>
            
        </Drawer.Navigator>
    )
}
```

## Drawer screenOption 속성
### drawerPosition
- 서랍의 위치 설정 : left,right
### drawerType
- 서랍 열릴때 애니메이션 방식과 형식 설정
- front : 뒤에있는 화면은 고정된체 서랍이 열린다
- slide : 서랍이 열리는 만큼 뒤 화면도 옆으로 밀린다.
- back : 서랍이 뒤쪽에 고정된 상태로, 본문이 위로 이동한다
- permanent : 서랍이 화면에 항상 고정
### drawerStyle
- 서랍의 스타일 설정
- backgroundColor: Drawer 메뉴의 배경 색상을 지정한다.
- width: Drawer의 너비를 설정한다.기본적으로 화면에서 Drawer가 차지하는 공간의 크기를 픽셀 단위로 조정한다.
- height: Drawer의 높이를 설정한다. 기본적으로 Drawer는 화면 높이를 전부 차지하지만,  특정 높이만큼만 Drawer를 나타내고 싶을 때 유용하다.
- borderWidth: Drawer의 테두리 두께를 설정한다.
- borderColor: Drawer의 테두리 색상을 지정한다.

### drawerLabelStyle
- 서랍의 메뉴의 라벨 텍스트 스타일 설정
- fontSize: 각 메뉴 항목의 글꼴 크기를 설정할 수 있다.