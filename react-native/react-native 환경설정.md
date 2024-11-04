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
- https://nodejs.org/ko

## Python 설치
- 리엑트네이티브 빌드때 파이썬 필요
- 파이썬 홈페이지에서 최신버전 다운로드

## JDK 설치 
- 오라클 홈페이지에서 설치
- https://www.oracle.com/kr/java/technologies/downloads/

## 안드로이드 스튜디오
- https://bit.ly/android-ide-download 에서 설치
- 환경변수 설정 : 변수이름 ANDROID_HOME, 변수값 C:\Users\사용자\AppData\Local\Android\Sdk
 <br/> Path 편집 C:\Users\lis\AppData\Local\Android\Sdk\platform-tools

### 에뮬레이터
- 안드로이드 스마트폰을 가상으로 만들어 앱 테스트 하는 프로그램
- 안드로이드스튜디오 -> More Action -> Virtual Device Manager

## 에디터 설치
- VSCODE 설치 : https://code.visualstudio.com/

## 리엑트네이티브 프로젝트 만들기
 
1. Expo를 사용하는 방법 : 
 - Expo CLI 설치 : npm install -g expo-cli 
 - Expo 프로젝트 생성 : expo init 프로젝트이름
 - Expo 프로젝트 실행 : cd 프로젝트이름 -> npm expo start 
2. 리엑트 네이티브 CLI 를 사용하는방법