# Controller 만들기

<hr/>

## 필요한 어노테이션
1. @RestController
@Controller와 @ResponseBody의 결합

2. @RequestMapping(" ") 
들어온 요청을 특정 메서드와 매핑하기 위해 사용하는 어노테이션

3. @GetMapping(" ")  @PostMapping(" ")  @PutMapping  @DeleteMapping
해당 경로로 각 Get,Post,Put,Delete 요청시 함수 실행

```
@RestController  //@Controller와 @ResponseBody의 결합
@RequestMapping("test")  //리소스
public class TestController {

	@GetMapping("/testGetMapping")  //해당 경로로 Get요청시 함수 실행
	public String testController() {
		return "Hello World testGetMapping";
	}
}
``` 

4. @PathVariable
동적경로처리 : 주소에 {}부분에 들어간 데이터를 파라미터로 받아서 함수 처리하는 어노테이션

```java
@RestController
public class OrderController {

    @GetMapping("/users/{userId}/orders/{orderId}")  // "/users/10/orders/30" 이라면
    public String getOrderByUserAndOrderId(@PathVariable("userId") Long userId,  //10 들어가고
                                           @PathVariable("orderId") Long orderId) {  //30 들어감
        return "User ID: " + userId + ", Order ID: " + orderId;
    }
}
```

5. @RequestParam
쿼리파라미터(?key=value)를 메서드의 파라미터로 받아서 함수 처리하는 어노테이션

```java
@RestController
public class UserController {

    @GetMapping("/users")
    public String getUserById(@RequestParam("id") Long userId, defaultValue = "0") {  //기본값 설정 가능
        return "User ID: " + userId;
    }
}
```

