# 내장 함수 객체

## map()
- 배열.map((item)=> 반복실행문 )
- 반복되는 컴포넌트를 렌더링하기 위해 사용 (for 대신 사용가능)
```js
const array = [1, 2, 3, 4, 5];

const listItems = array.map((item) =>
  <li>{item}</li>
);

return (
  <ul>{listItems}</ul> 
);
```

## filter()
- 객체명.filter((item)=> 조건문)
- 메서드는 주어진 함수의 테스트를 통과하는 모든 요소를 모아 새로운 배열로 반환
```js
const todoList = [
    { taskName: "방 청소", finished: false },
    { taskName: "화장실 청소", finished: true },
  ];

  return (
     <>
      {todoList
        .filter((todo) => todo.finished === false)
        .map((todo, i) => (
          <div key={todo.taskName}>{todo.taskName}</div>
        ))}
    </>
  );
```
## find()
- 배열.find(item=>조건)
- 배열의 요소를 순차적으로 순회하면서 조건에 일치하는 요소의 값을 즉시 반환
```js
const result1 = arr1.find(item => item>30);
```

## Math
- 수학적인 상수와 함수를 위한 속성과 메서드를 가진 내장 객체

