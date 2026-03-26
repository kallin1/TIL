# [2026-03-26] Spring Boot 설계: 관심사의 분리 (SoC)를 통한 계층 구조 개선

## 📝 정보기록
- **개념 요약**: Controller는 외부 통신과 DTO 포장을, Service는 순수 비즈니스 로직만을 담당하도록 분리하여 계층 간 결합도를 낮춤. 
이렇게 설계하면 서비스가 특정 API 응답 규격(DTO)에 의존하지 않게 되어 나중에 다른 곳(배치 작업 등)에서 서비스 재사용이 용이해진다.
- **핵심 코드**:

  ```java
  // Service: DTO 의존성 없이 순수 데이터 반환
  public String repeatString(String input) { return input; }
  
  // Controller: 서비스 결과를 받아 DTO로 포장하여 반환
  String result = demoService.repeatString(request.getValue());
  return new RepeatResponse(result, result);

