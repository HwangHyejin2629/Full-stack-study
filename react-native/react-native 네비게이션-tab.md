# 탭 네비게이션
- npm install @react-navigation/bottom-tabs@6.5.20 --force
- import { createBottomTabNavigator } from "@react-navigation/bottom-tabs";
- 이동할때 네비게이션 주지 않는다.

## 아이콘 설정하기
```js
import {MaterialCommunityIcons} from '@expo/vector-icons'

const TabIcon = ({name, size, color}) => {
    return <MaterialCommunityIcons name={name} size={size} color={color} />;
}



const Tab = createBottomTabNavigator();

const TabNavigation = () => {
    return (
      <Tab.Navigator
      initialRouteName='Settings'>
        <Tab.Screen 
            name="Mail" 
            component={Mail}
            options={{
                tabBarIcon: props => TabIcon({...props, name:'email'}),
            }} />
        <Tab.Screen 
            name="Meet" 
            component={Meet}
            options={{
                tabBarIcon: props => TabIcon({...props, name:'video'}),
            }} />
        <Tab.Screen 
            name="Settings" 
            component={Settings}
            options={{
                tabBarIcon: props => TabIcon({...props, name:'settings'}),
            }} />
      </Tab.Navigator>
    );
  };

  export default TabNavigation;
```

## 라벨수정하기
```js
<Tab.Screen name="Mail" component={Mail} options={{tabBarLabel:'Inbox'}} />
```

