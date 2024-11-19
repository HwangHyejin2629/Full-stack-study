# 배포

## app.json 수정
- name : 프로젝트 이름 name을 사용자에게 보여주고 싶은 이름으로 수정, 꼭 수정할 필요는 없음
- version : 어플리케이션 버전을 관리할 값, ios와 안드로이드 모두 적용되는 버전, 각 플랫폼의 내부 버전 번호를 나타내는 ios의 buildNumber와 android의 versionCode가 추가로 필요하다.
- ios 의 bundleldentifier 와 android 의 package 값들은 어플리케이션을 구분하는 고유 값으로 다른 어플리케이션과 구분하는 역할을 하기때문에 유일한 값으로 입력해야한다. 회사 이름이나 도메인을 많이 사용하고, 도메인을 사용하는 경우 주소를 반대로 기재한 형태로 사용

### 권한
- expo로 만든 프로젝트는 안드로이드에 대한 권한을 가지고 있기 때문에 반드시 설정하는 값은 아니다 꼭 필요한 권한만 지정하기 위해 permission속성을 지정할 수 있다.

## assets 
- icon.png 

## build
- expo build:android

- EAS(build)를 사용하도록 권장하고 있다 최신 Expo기능과 네이티브 코드 수정 지원을 제공하며, GooglePlay와의 호환성이 더 뛰어나다

- npm install -g eas-cli
- eas init
- 권한 없으면 git bash 

## eas.json
```js
{
    "cli": {
      "version": ">= 3.0.0"
    },
    "build": {
      "production": {
        "android": {
          "buildType": "app-bundle"
        },
        "ios": {
          "simulator": false
        }
      },
      "preview": {
        "android": {
          "buildType": "apk"
        }
      }
    }
  }
```


## 구글 배포
- Google Play Console -> 개발자 개정 생성 -> 앱 만들기 ->eas build --platform android --profile preview -> 앱관련 정보