# 조건문
- 조건이 참인경우:  true, 0과 null false undefined가 아닌 모든 값
- 거짓인경우는 0, null, false, undefined 인경우
## if 조건문
- if(조건){조건해당시 실행문} else if(조건){조건해당시 실행문} else{다 해당안될때 실행문}
```js
{(()=>{
    if(name ==='Hanbit') return 'My name is Hanbit';
    else if(name === 'Gil-Dong') return 'My name is Gil-Dong';
    else return 'My name is React Native';
})()}
```
## 삼항연산자
- 조건1 ? 조건1이 참일때 반환값 : 조건2 ? 조건2가 참일때 반환값 : 거짓일때 반환값
```js
<Text style={styles.text}>
    My name is {name === 'Gil-Dong' ? 'Gil-Dong Hong' : 'React-native'}
</Text>
```
## && || 연산
- &&  앞의 조건이 참일 때 뒤의 내용이 렌더링 되고, 거짓인 경우 나타나지 않는다.
```js
{name === 'Gil-Dong' &&(
    <Text style={styles.text}> My name is Gil-Dong</Text>
)}
```
- ||  앞의 조건이 거짓인 겨우 뒤에 내용이 렌더링 됨
```js
<Text>{name || "Default Name"}</Text>
```