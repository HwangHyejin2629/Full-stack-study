# hook

<hr>

## useState
- const[state, setter]=useState(초기값)
- setter함수는 비동기라 여러번 호출시 반영 안될 수 있다.
- 그래서 함수 형식으로 이전 상태를 어떻게 바꿀껀지 설정 : setter(prev=>prev+1)
- 객체가 새로 만들어져야 수정됐다고 생각하기 때문에 state 사용를 사용한다.
- 화살표 함수로 호출 : 화살표 없이 하면 컴포넌트가 렌더링 되자마자 실행된다.
```js
onPress={()=>setCount(count+1)}
```
- 파라미터에 함수 전달해서 setter 사용하자, 
<br/>상태가 여러번 일어날 경우 상태 변경전에 다시 상태에 대한 업데이트 발생하는 경우 방지
```js
setState(prevState => {});
```
<hr>

## useEffect
```js
useEffect(()=> {실행문}, [state1, state2]) 
```
- 첫번째 인자 : 어떤 조건하에 하고자 하는 함수
- 두번째 인자 : 언제 실행될건지 조건을 정하는 배열 (의존성 배열)
<br/> 없을때 : 매 랜더링마다, [] : 마운트 될때 실행, [state] : state가 변경될때마다

- 컴포넌트가 렌더링 될때마다 원하는 작업 실행되도록 설정
- useEffect 자체가 비동기 동작을 직접적으로 지원을 안함

### 클린업함수
- useEffect(()=>{
    실행문
    return ()=>{}  -----클린업함수
})
- 클린업 함수 : 컴포넌트가 언마운트 되거나, useEffect가 다시 실행되기 전에 실행
- 리소스를 정리, 이벤트리스너 제거하거나, 타이머 정하기 위해 사용한다.

### useEffect 첫번째 요소인 함수에 비동기 함수가 안되는이유
- useEffect(async()=> 실행문) --- X 
- useEffect(()=>{ const asc = async()=> 실행문}) ---- 안에 함수를 선언해서 사용
1. useEffect 자체가 비동기 동작을 직접적으로 지원을 안함
2. useEffect의 반환값은 반드시 클린업함수 또는 undefined 여야한다.
비동기 함수를 사용하면 반환값이 promise 가 된다. (규칙 위반)
3. 비동기 흐름으로 인한 예기치 않은 동작
- 비동기 함수가 실행되는 동안 컴포넌트가 재랜더링 될때 상태가 변화해서 데이터가 꼬이거나, 메모리 누수 가능.
```js
useEffect(()=>{
    //직접 걸지 않고 안에 함수 만듦
     const fetchData=async()=>{
        try {
            const res= await fetch(url); //url에 비동기 통신요청(default 는 GET 방식)
            const result= await res.json(); //fatch를 통해 얻어온 데이터는 json 형식으로 변환해야한다.
                if(res.ok){
                setData(result)
                setError(null)
            }else{
                throw result;
            }
        } catch (error) {
            setError(error)
        }
    }
    fetchData() //fetchData 호출
},[])
```
<hr>

## useRef
- const ref=useRef() 
1.  특정 엘리먼트 선택할 수 있다.(querySelector처럼 태그 선택 가능)
```js
const refName=useRef(null) // ------{current:null}
<StyledInput ref={refName}>
```
2. 리렌더링 없이 상태 유지할때 사용 : useRef 값이 바뀌어도 재 렌더링이 되지 않기 때문에 값이 바뀌어도 렌더링 필요하지 않은 경우 사용 
- ex 타이머, 이전 값 추적, 스크롤 위치 추적

<hr>

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
<hr>

## useReducer()
- 현재 상태와 상태를 어떻게 업그레이드 할지를 정의한 함수를 통해 새로운 상태를 변환

### 주요개념
- state : 현재 컴포넌트의 상태값
- action : 상태를 어떻게 변경할지 나타내는 명령
- reducer : 현재 상태와 액션을 받아서 새로운 상태를 반환하는 함수

```js
const initialState={count:0}  //초기값
const[state,dispatch]=useReducer(reducer, initialState)  
//처음은 초기값 initialState가 stata로 들어간다
function reducer(state,action){
    switch(action.type){
        case 'INCREMENT' return {count:state.count+1};
        case 'DECREMENT' return {count:state.count-1};
    }
 }

// dispatch는 action에 전달하는 역할
<Button onClick={()=> dispatch({type:'INCREMENT'})}>
<Button onClick={()=> dispatch({type:'DECREMENT'})}>
```

### 언제 사용? 
1. 상태가 여러개일때 : useState로 각각 관리하기보다 하나의 state객체로 묶어 관리
2. 복잡한 로직이 필요할때 : 상태 변경에 따라 다양한 조건을 검토, 여러단계를 거쳐 상태 변경이 필요할때
3. 상태 업데이트 로직을 컴포넌트 밖으로 분리하고 싶을때 : reducer함수는 컴포넌트 외부에도 둘 수 있어 상태 관리 로직을 명확히 분리


