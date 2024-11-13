# props

## props 전달하고 사용하기

- <컴포넌트명 속성="값">  : 속성과 값을 prop로 전달한다. props.속성
```js
<Button title="button" onPress={()=> alert('Click!!')}/>
//Button 컴포넌트에서 title과 onPress를 받아서 사용할 수 있다.
```
 
- <컴포넌트명> 내용 </컴포넌트명> : 태그 사이의 값은 자식컴포넌트의 props. children으로 전달된다.

```js
<Text style={{color: 'white', fontSize : 24}}>{props.children || props.title}</Text>
//props에 children이 있으면 children 우선시하도록 작성
```

## defaultProps
- 컴포넌트명.defaultProp={키:값}
```js
const MyButton = (props) => {

    MyButton.defaultProps = {
        title: 'Button',
    }
...
```

## PropsTypes
- props의 타입을 잘못 전달하거나 필수로 전달해야하는 값을 누락시킬경우 경고메세지 보내는 방법
- npm install prop-types
- 타입 오류 설정 : 컴포넌트명.propTypes={키:PropType.타입종류}
- 필수 오류 설정 : 컴포넌트명.propTypes={키:PropType.func.isRequired}

```js
import PropTypes from 'prop-types'

Image.defaultProps = {
    rounded: false,
    showButton: false,
    onChangeImage:()=>{}
}

Image.propTypes = {
    uri: PropTypes.string, //uri에 들어오는 값은 string 이어야 해
    imageStyle: PropTypes.object,
    rounded: PropTypes.bool,
    shoeButton: PropTypes.bool,
    onChangeImage:PropTypes.func,
}
```


