# [2026-03-26] Lombok 생성자 어노테이션과 객체지향적 Getter/Setter 활용

## 📝 정보기록
### 💡 롬복(Lombok) 생성자 어노테이션 3종
1. **@NoArgsConstructor**: 파라미터가 없는 **기본 생성자**를 생성함. 
   - *용도*: JPA 엔티티나 JSON 라이브러리(Jackson)가 객체를 생성할 때 내부적으로 필요함.
2. **@AllArgsConstructor**: **모든 필드**를 파라미터로 받는 생성자를 생성함.
   - *용도*: 객체의 모든 값을 한 번에 초기화하며 생성할 때 사용함.
3. **@RequiredArgsConstructor**: **`final`이 붙은 필드만** 파라미터로 받는 생성자를 생성함.
   - *용도*: 스프링의 **의존성 주입(DI)** 시 생성자 주입 방식을 간결하게 만들기 위해 사용함.

### 💡 Getter와 Setter의 개념 및 지향/지양
- **Getter**: 객체의 필드 값을 읽어오는 메서드. (데이터 조회 및 응답 시 필수적)
- **Setter**: 객체의 필드 값을 변경하는 메서드. (데이터의 불변성을 해치고 변경 의도를 파악하기 어렵게 만드므로 지양한다.)

### 💻 핵심 코드 예시 (생성자 주입 및 Getter 활용)
```java
@RestController
@RequiredArgsConstructor // final 필드인 서비스 주입을 위한 생성자 자동 생성
public class RepeatController {
    private final DemoService demoService; // 생성자 주입 대상

    @PostMapping("/api/repeat")
    public RepeatResponse repeat(@RequestBody RepeatRequest request) {
        // Getter를 통해 데이터를 꺼내어 서비스에 전달
        String result = demoService.repeatString(request.getValue()); 
        return new RepeatResponse(result);
    }
}
