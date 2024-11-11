# 옵셔널체이닝

- 객체, 배열, 함수에 안전하게 접근하기위해, 속성이 존재하지 않아도 에러를 발생시키지 않도록 undifind를 반환한다. (try catch 없이 에러처리 가능)
- 중첩된 객체에 간단하게 접근이 가능하다.
- ?. : const 변수명 = 객체.키1.키1-1

```js
const user = {
    profile: {
        name: "Alice"
    }
};

// 옵셔널 체이닝을 통해 더 간단하게 안전하게 접근 가능
const age = user.profile?.hobby;
console.log(hobby); // undefined (hobby는 없으니까)
```
```js
const users = [{ name: "Alice" }, null, { name: "Bob" }];

// 옵셔널 체이닝으로 더 간결하게 배열 요소에 접근 가능
const userName = users[1]?.name;
console.log(userName); // undefined (null이니까)
```

