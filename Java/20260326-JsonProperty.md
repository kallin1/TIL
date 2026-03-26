# [2026-03-26] @JsonProperty를 통한 API 스펙의 안정성 확보

## 📝 정보기록
- **개념 요약**: Java 객체의 필드와 JSON 데이터의 키값을 명시적으로 매핑해주는 어노테이션.
- **핵심 코드**: 
  ```java
  @Getter
  @NoArgsConstructor
  public class RepeatRequest {
      @JsonProperty("value") // JSON의 "value" 키를 이 필드에 강제 매핑
      private String value;
  }
