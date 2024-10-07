

# Service 레이어 만들기


## 필요한 어노테이션
### @Service <br/>
서비스 클래스임을 알려주는 어노테이션 @Component 의 자식 어노테이션
@Component : bean생성하는 어노테이션

```java
package com.example.demo.service;

import org.springframework.stereotype.Service;

@Service 
public class TodoService {

	public String testService() {
		return "Test Service";
	}
}
```
Controller에 Service 적용
```java
@RestController
@RequestMapping("todo")
public class TodoController {

	@Autowired
	private TodoService service;  // 서비스 객체생성
	
	@GetMapping("/test")
	public ResponseEntity<?> testTodo(){
		String str = service.testService();// 서비스의 메서드 실행
		List<String> list = new ArrayList<>();
		list.add(str);
		ResponseDTO<String>response = ResponseDTO.<String>builder().data(list).build();
		return ResponseEntity.ok().body(response);
		
	}
}
```