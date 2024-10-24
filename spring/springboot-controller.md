

# Controller 레이어


## 필요한 어노테이션
### @RestController <br/>
@Controller와 @ResponseBody의 결합  
@Controller : Controller 클래스임을 알려주는 어노테이션, @Component 의 자식 어노테이션
@ResponseBody :  자바객체를 HTTP응답 본문 객체로 변환하여 서버에서 클라이언트에게 전송
@Component : bean생성하는 어노테이션

### @RequestMapping(" ") <br/>
들어온 요청을 특정 메서드와 매핑하기 위해 사용하는 어노테이션

### @GetMapping(" ")  @PostMapping(" ")  @PutMapping  @DeleteMapping <br/>
해당 경로로 각 Get,Post,Put,Delete 요청시 함수 실행

```java
@RestController  //@Controller와 @ResponseBody의 결합
@RequestMapping("test")  //리소스
public class TestController {

	@GetMapping("/testGetMapping")  //해당 경로로 Get요청시 함수 실행
	public String testController() {
		return "Hello World testGetMapping";
	}
}
``` 

### @PathVariable <br/>
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

### @RequestParam <br/>
쿼리파라미터(?key=value)를 메서드의 파라미터로 받아서 함수 처리하는 어노테이션
required=false : 필드에 적용되지 않아도 예외 발생하지 않음
defaultValue : 기본값 설정

```java
@RestController 
public class UserController {

    @GetMapping("/users")  //users/?id=123&&... ->userId 에 123 들어감
    public String getUserById(@RequestParam(required=false) Long userId, defaultValue = "0") {
        return "User ID: " + userId;
    }
}
```

### @RequestBody  <br/>
HTTP 요청 본문 body데이터와 JSON 데이터를 자바 객체로 변환하여 컨트롤러 메서드의 매개변수로 전달하는 어노테이션
<-> @ResponseBody

```java
public class UserApiController {

    @PostMapping
    public ResponseEntity save(@RequestBody UserRequestDto requestDto) {  
        //requestDto 에 body 데이터 객체로 담음

    }
}
```



## 필요한 클래스



### ResponseEntity  <br/>
HTTP 응답을 세밀하게 제어할 수 있는 방법 
우리가 작성할 컨트롤러는 모두 ResponseEntity를 반환한다.
- 상태코드 제어
- 헤드 제어
- 응답 본문 제어

주요메서드 
- ResponseEntity.ok(): 200 OK 상태 코드로 응답하는 빌더 메서드. ---자주씀
- ResponseEntity.status(HttpStatus status): 특정 상태 코드를 반환하는 빌더 메서드.
- ResponseEntity.noContent(): 204 No Content 응답을 반환하는 메서드.
- ResponseEntity.badRequest(): 400 Bad Request 응답을 반환하는 메서드. ---자주씀
- ResponseEntity.notFound(): 404 Not Found 응답을 반환하는 메서드.

```java
@GetMapping("/testResponseEntity")
	public ResponseEntity<?> testControllerResponseEntity(){
		List<String> list = new ArrayList<>();
		list.add("Hellow World! I'm ResponseEntity. And you got 400");
		ResponseDTO<String>response = ResponseDTO.<String>builder().data(list).build();
		//http status를 400으로 설정
		return ResponseEntity.badRequest().body(response);
	}
```
### List <br/>
배열과 같이 객체를 일렬로 늘어놓은 구조
여러개의 객체를 담아 전달해야 하는 경우 사용

```java
@GetMapping("/testResponseBody")
	public ResponseDTO<String> testControllerResponseBody(){
		List<String> list = new ArrayList<>();
		list.add("Hellow World! i'm ResponseDTO");
		ResponseDTO<String> response = ResponseDTO.<String>builder().data(list).build();
		return response;  //DTO로 담아서 내보낸다(규칙)
        //ResponseDTO<String> response : 문자열 리스트를 담은 ResponseDTO
	}
```
