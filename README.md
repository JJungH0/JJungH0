## 👤 About Me on Book1lluwa — by 최정환

**포지션**: 쿠폰/이벤트 도메인 개발 · 운영 자동화  
**핵심 기술스택**: Spring Boot, JPA, Spring Scheduler, RabbitMQ, Redis, MySQL, GitHub Actions, SonarQube

### 💥 내 역할 요약
- **쿠폰 도메인 전담**: 쿠폰 **CRUD**, 발급/사용 정책, 이력/에러 로깅
- **운영 자동화**: 
  - **생일 자동발급** — Spring Scheduler로 매일 00시 대상 회원 일괄 발급
  - **가입 이벤트 실시간 발급** — 회원가입 이벤트 → **RabbitMQ** 소비자로 비동기 발급
- **확장성 설계**: 대량 트래픽 시에도 발급 병목을 피하도록 **큐 기반 처리** 및 **재시도 정책** 적용
- **신뢰성 확보**: 발급/사용 히스토리 모델링, 장애 상황 **상세 로깅**으로 근본 원인 분석 단축

### 🧩 설계 포인트 (왜 이렇게 설계했나?)
- **동기 발급 → 비동기 전환(RabbitMQ)**  
  결제/가입 등 핵심 트랜잭션이 **쿠폰 발급 지연**에 끌려가지 않도록 분리.  
  실패 시 **DLQ(사망 큐)** 로 격리 → 재처리/모니터링 가능.
- **스케줄러 기반 자동 집행**  
  마케팅성 쿠폰(생일/기념일)은 **스케줄러 + 배치성 처리**가 운영비를 낮춤.
- **이벤트 소싱에 준한 이력화**  
  발급/사용/취소/만료 등 상태 전이를 모두 기록 → 문제 재현과 고객 CS 응대가 쉬워짐.

### 🔎 대표 구현(코드 스니펫 가이드)
> 아래는 제가 구현한 핵심 흐름을 **의사 코드**로 간단히 보여줍니다.  
> (실제 프로젝트 코드에선 패키지/예외/검증/트랜잭션 경계가 더 정교합니다.)

```java
// 쿠폰 발급 메시지 소비자 (RabbitMQ Consumer)
// 역할: 회원가입 이벤트 수신 → 쿠폰 발급 서비스 호출
@RabbitListener(queues = "coupon.issue.memberSignUp")
public void handleMemberSignUpEvent(MemberSignUpEvent event) {
    // 1) 이벤트 유효성 검증
    // 2) 중복 발급 방지 로직 (이벤트ID / 회원ID 기준 멱등성 보장)
    // 3) 쿠폰 발급 서비스 호출
    couponService.issueWelcomeCoupon(event.getMemberId());
}
