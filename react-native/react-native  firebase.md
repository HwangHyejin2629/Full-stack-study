# firebase 

## NoSQL (Not Only SQL)
- SQL 데이터베이스는 관계형인 반면 NoSQL 데이터베이스는 비 관계형
- 높은 확장성과 가용성 : 사전에 스키마를 정의하지 않아도 저장됨
- 실시간 웹 애플리케이션 및 빅 데이터에 널리 사용
- 클라우드에 특화 aws에서는 rds랑 비슷한느낌
- MongoDB도 NoSQL중하나, 클라우드 컴퓨터에 설치해도 사용가능


### 구성요소
- 테이블이나 행이 없고, 컬랙션, 문서, 필드로 구성된다.
- 컬랙션 : 테이블의 역할,문서의 컨테이너역할(감싸는 역할), 모든 문서는 항상 컬랙션에 저장되어야한다. 여러문서를 포함한다.
- 문서 : 컬랙션에 속하는 단일 데이터단위, row(행)의 역할, 문서 안에는 데이터를 키-값 쌍 데이터(필드)나 하위컬랙션이 있다.
- 필드 : 키-값의 쌍, column(열)의 역할, 문서내에서 데이터를 정의하는 개별 속성, 문서마다 필드가 다를수 있다.
- 컬랙션과 문서는 항상 유일한 ID를 가지고 있어야한다.

### RDBMS 와 NoSQL 비교
#### RDBMS 
- 스키마 기반 설계로 데이터 구조가 고정적이고 일관성을 유지하기 쉽니다.   
- 트랜잭션 사용에 강점
- 관계형 데이터 모델 -> 테이블간 관계를 명확히 정의하고 복잡한 쿼리나 JSON을 통해 데이터를 쉽게 검색
- SQL 대부분 RDBMS에서 사용되므로 표준화된 쿼리를 작성할 수 있다.
- 단점 : 확장성에 제한, 유연성이 부족(스키마 변경이 어렵다)-> 빠르게 변환하는 어플리케이션에 적합하지 않다.
- 사용시 : 금융, 인사관리 시스템, 기존 데이터베이스와 통합

#### NoSQL
- 유연한 모델, 스키마가 없어서 구조가 자주 바뀌는 형태
- 문서, 키-값, 그래프 등 다양한 데이터 모델 지원
- JSON, XML 등 비정형 데이터 처리에 적합
- 사용시 : 빅데이터 처리, 유연한 데이터 모델이 필요할때, 빠른 확장이 필요할때

## 주요기능과 서비스
###  Authentication 
- 다양한 인증 방식을 지원하여 사용자의 로그인과 회원가입을 간편하게 구현
- 이메일/비밀번호, 전화번호, 소셜 로그인(Google, Facebook, Twitter 등), 익명 인증 등을 제공

- 인증 사용하기 : firebase -> Authentication -> 로그인 방법 설정 버튼 -> 이메일/비밀번호 버튼 토글활성화 -> 저장


### Realtime Database
- 클라우드 기반의 NoSQL 데이터베이스로 데이터가 실시간으로 동기화 된다.
- 실시간 채팅, 라이브 업데이트 기능

### Cloud Firestore
- NoSQL 문서 중심의 데이터베이스
- 문서 중심의 데이터베이스
- Realtime Database와 유사하지만 더 강력하고 복잡한 쿼리를 지원
- 데이터베이스를 서버에 배포하지 않고도 대규모 데이터베이스를 관리
- 데이터베이스 사용하기 : firebase -> Cloud Firestore-> 지역 설정 asia-northeast3(서울) -> 요금제 설정 -> 지역설정(가까운지역선정) 

### Storage
- 이미지, 동영상, 파일 등을 저장하고 관리할 수 있는 클라우드 스토리지 서비스
- 위치 서울로 설정
- 사용할 이미지 파일 업로드하여 사용 가능 : url token 부분을 제외하고 사용 (firebascstorage.googleeapis.com.....app/o)


### Cloud Messaging (FCM)
- 푸시 알림을 전송할 수 있는 무료 메시징 서비스
- 사용자에게 실시간 알림을 보낼 때

### Hosting
- 정적 웹사이트나 단일 페이지 애플리케이션(SPA)을 위한 빠르고 안전한 호스팅 서비스
- Firebase CLI를 통해 빠르게 배포할 수 있으며, SSL 인증서가 자동으로 적용되어 안전한 HTTPS 통신을 제공

### Cloud Functions
- 서버리스 환경에서 백엔드 코드를 실행할 수 있는 기능
- 이벤트 기반으로 트리거되는 함수로, 데이터베이스 변경, 인증, FCM 등을 활용하여 백엔드 로직을 처리할 수 있다.




## 파이어베이스 사용하기
- https://console.firebase.google.com/
- 프로젝트 만들기 -> 이름지정, 약정체크 -> 파이어베이스를 사용하기 위한 설정값을 root 에 firebase.json 생성후 코드 추가

```json
{
  "apiKey": "...",
  "authDomain": "...",
  "projectId": "...",
  "storageBucket": "...",
  "messagingSenderId": "...",
  "appId": "...",
  "measurementId": "..."
}
```
- .gitignore 에 추가하기
```
...
# firebase
firebase.json
```

## 라이브러리 사용

- npm install firebase --legacy-peer-deps --force
```js
import * as firebase from 'firebase'
import config from '../../firebase.json'

const app = firebase.initializeApp(config);
```

