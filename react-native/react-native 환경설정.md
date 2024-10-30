# 리엑트 네이티브 환경설정
## 리엑트 네이티브 
- react 기반 ios, 안드로이드 앱 모두 제작 가능
- window에서는 안드로이드만 가능, mac에서는 둘다 가능하다.
- JSX : HTML처럼 생긴 자바스크립트, 바벨로 자바스크립트 코드로 변환된다.

```js
function formatName(user){
   return user.firstName + ' '+ user.lastName;
}

const User = {
   firstName : 'Beomjun',
   lastName : 'kim'
};

//JDK
const element = <h1>hello, {formatName(user)}!</h1>

//JS
const element = /*#_PURE_*#/ React.createElement(
'h1',
null,
'Hello, ',
formatName(user),
'!'
)
```

## Node.js 설치
- LTS로 설치 : Long Term Service 오랜기간 지원하는 버전, 안정적이다. (최신버전 사용)
- 노드 설치가 되면 npm 도 같이 설치된다.

## Python 설치
- 리엑트네이티브 빌드때 파이썬 필요
- 파이썬 홈페이지에서 최신버전 다운로드

## JDK와 
- JDK : JRE(JVM),lib

## 안드로이드 스튜디오
- https://bit.ly/android-ide-download 에서 설치
- custom 선택 -> Android SDK, Android API 35, Performance (intel HAXM), Android Virtual Device 선택 
- 안드로이드 스튜디오 실행 -> More Action -> SDK Manager
