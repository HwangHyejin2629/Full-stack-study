# hook

## useState
- const[state, setter]=useState(초기값)
- setter함수는 비동기라 여러번 호출시 반영 안될 수 있다.
- 그래서 함수 형식으로 이전 상태를 어떻게 바꿀껀지 설정 : setter(prev=>prev+1)
- 객체가 새로 만들어져야 수정됐다고 생각하기 때문에 state 사용를 사용한다.

## useEffect
- useEffect(()=> {실행문}, [state1, state2]) 
- 첫번째 인자 : 어떤 조건하에 하고자 하는 함수
- 두번째 인자 : 언제 실행될건지 조건을 정하는 배열 (의존성 배열)
<br/> 없을때 : 매 랜더링마다, [] : 마운트 될때 실행, [state] : state가 변경될때마다
- 컴포넌트가 렌더링 될때마다 원하는 작업 실행되도록 설정

### 클린업함수
- useEffect(()=>{
    실행문
    return ()=>{}  -----클린업함수
})
- 클린업 함수 : 컴포넌트가 언마운트 되거나, useEffect가 다시 실행되기 전에 실행
- 리소스를 정리, 이벤트리스너 제거하거나, 타이머 정하기 위해 사용한다.
- useEffect는 첫번째 인자로 함수를 받는데, 이 함수는 다시 함수를 반환할 수 있다. 반환된 함수가 클린업 함수

## useRef
- const ref=useRef() 
1.  특정 엘리먼트 선택할 수 있다.(querySelector처럼 태그 선택 가능)
```js
const refName=useRef(null) // ------{current:null}
<StyledInput ref={refName}>
```
2. 리렌더링 없이 상태 유지할때 사용 : useRef 값이 바뀌어도 재 렌더링이 되지 않기 때문에 값이 바뀌어도 렌더링 필요하지 않은 경우 사용 
- ex 타이머, 이전 값 추적, 스크롤 위치 추적

## useMemo
- useMemo(()=>{},[])
- 특정 연산 결과를 저장해두고, 필요시 꺼내 씀, 불필요한 반복 계산을 피한다.
- 의존성 배열에 따라 값이 바뀔때만 연산 다시 수행하도록 설정가능
```js
const list = ['JavaScript', 'Expo', 'Expo', 'React Native'];

const Length = () => {
  const [text, setText] = useState(list[0]);

  const _onPress = () => {
    ++idx;
    if (idx < list.length) setText(list[idx]);
  };
  const length = useMemo(() => getLength(text), [text]);
}
```
```js
const [query, setQuery] = useState('');
const items = Array.from({ length: 1000 }, (_, i) => `Item ${i + 1}`); // 큰 배열 예시

// query가 변경될 때만 필터링 작업을 수행
const filteredItems = useMemo(() => {
    console.log("Filtering items...");
    return items.filter(item => item.toLowerCase().includes(query.toLowerCase()));
}, [query]);
```

