<div align="center">

![banner](https://capsule-render.vercel.app/api?type=waving&color=gradient&height=200&section=header&text=최정환's%20GitHub%20Portfolio&fontSize=40&fontAlign=50&fontAlignY=35)

</div>

---

## 👨‍💻 About Me — 최정환

안녕하세요!  
저는 **Spring Boot 기반의 MSA 아키텍처 서비스 개발**을 경험한 백엔드 개발자 취업 준비생 **최정환**입니다.  
대규모 트래픽 환경에서 안정적이고 확장 가능한 시스템을 설계·운영하는 데 관심이 많습니다.  
꾸준한 학습과 지식 공유, 협업을 통해 함께 성장하는 것을 중요하게 생각합니다.

---

## 🛠 Tech Stack
- **Languages**: Java
- **Frameworks**: Spring Boot, Spring Cloud (Gateway, Config, Eureka), Spring Batch, JPA/Hibernate
- **Infra / Ops**: GitHub Actions, Nginx, SonarQube, 무중단 배포(롤링)
- **Messaging / Cache**: RabbitMQ
- **Database**: MySQL
- **Collaboration**: GitHub Issue/PR 기반 협업, 코드 리뷰, 테스트 자동화

---
## 📈 Contribution Graph

<p align="center">
  <img
    src="https://github-readme-activity-graph.vercel.app/graph?username=JJungH0&theme=react-dark&area=true&hide_border=true"
  />
</p>

---

## 📚 프로젝트 경험

### Book1lluwa — 온라인 도서 쇼핑몰 (MSA 기반)
> 기간: 2025.06 ~ 2025.07  
> 역할: **쿠폰/이벤트 도메인 담당**

#### 🔑 기여
- 쿠폰 CRUD 및 정책(발급/사용/만료/취소) 설계·구현
- **Spring Scheduler** 기반 **생일 쿠폰 자동 발급**
- **RabbitMQ 기반 회원가입 이벤트 실시간 발급**
  - 멱등성 처리(Idempotency): 동일 이벤트가 여러 번 들어와도 **쿠폰은 1개만 발급**되도록 고유 키를 활용해 **중복 방지**
- **발급/사용/만료 이력 관리 + 에러 로깅 시스템 구축**
  - 모든 상태 전이를 기록해 **문제 재현·장애 원인 추적**이 용이
- **DLQ(Dead Letter Queue) 설계**
  - 처리 실패 이벤트를 별도 큐에 보관해 손실을 막고, **관리자가 재처리 가능**
  - 대규모 트래픽 환경에서도 안정성 확보

#### 💡 문제 해결 사례
- **문제**: 동기 방식 쿠폰 발급 시 회원가입/결제 API 응답 지연 및 실패 발생  
- **해결**: RabbitMQ 기반 **비동기 발급 구조** 전환, 멱등성 처리로 **중복 방지**, DLQ로 장애 이벤트 **안전 격리**  
- **결과**: 피크 타임에도 API 응답 속도 안정화, 발급 실패율 감소, 운영자가 장애를 신속히 추적·복구 가능  

🔗 [프로젝트 웹 홈페이지](https://book1lluwa.store) · [프로젝트 GitHub](https://github.com/nhnacademy-be10-1lluwa) · [API 명세](https://book1lluwa.store/docs.html) · [소개 영상](https://youtu.be/Mm8H87yzw7I) · [개인 Notion](https://bottlenose-balloon-0b4.notion.site/1b95c23e942f8197948befcbec5a50f4?v=1b95c23e942f8121b0e2000c57156735&source=copy_link)

---

## 🚀 성장 목표
- Kotlin · Spring WebFlux · Kafka 기반의 **실시간 대규모 트래픽 처리 시스템** 경험 확장
- Kubernetes, ArgoCD 등 **운영 자동화·클라우드 네이티브 환경** 심화 학습
- **성능 최적화 & 운영 효율화**를 통한 고가용성 시스템 설계 역량 강화
- 팀 내 지식 공유와 협업을 즐기는 **함께 성장하는 개발자**로 성장

---

<div align="center">

![footer](https://capsule-render.vercel.app/api?type=waving&color=gradient&height=150&section=footer)

</div>
