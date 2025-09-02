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

## 📊 GitHub Stats

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=JJungH0&show_icons=true&theme=radical" height="150" />
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=JJungH0&layout=compact&theme=radical" height="150" />
</p>

---

## 📚 프로젝트 경험

### Book1lluwa — 온라인 도서 쇼핑몰 (MSA 기반)
> 기간: 2025.06 ~ 2025.07  
> 역할: **쿠폰/이벤트 도메인 담당**

#### 🔑 기여
- 쿠폰 CRUD 및 정책(발급/사용/만료/취소) 설계·구현
- **Spring Scheduler** 기반 **생일 쿠폰 자동 발급**
- **RabbitMQ** 기반 **회원가입 이벤트 실시간 발급**, 멱등성 처리로 중복 방지
- 발급/사용/만료 이력 및 **에러 로깅 시스템** 구축 → 장애 원인 추적 단축
- DLQ(Dead Letter Queue) 설계로 **대규모 트래픽 안정성 확보**

#### 💡 문제 해결 사례
- **문제**: 동기 방식 쿠폰 발급 시 회원가입/결제 API 응답 지연 및 실패 발생  
- **해결**: RabbitMQ 기반 비동기 발급 구조 전환, 멱등키 적용, DLQ로 장애 격리  
- **결과**: 피크 타임에도 API 응답 속도 안정화, 발급 실패율 감소, 고객 경험 개선  

🔗 [프로젝트 Demo](https://book1lluwa.store) · [API 명세](https://book1lluwa.store/docs.html) · [소개 영상](https://youtu.be/Mm8H87yzw7I)

---

## 🚀 성장 목표
- Kotlin · Spring WebFlux · Kafka 기반의 **실시간 대규모 트래픽 처리 시스템** 경험 확장
- Kubernetes, ArgoCD 등 **운영 자동화·클라우드 네이티브 환경** 심화 학습
- **지속적인 성능 최적화 & 운영 효율화**를 통해 고가용성 시스템 설계 역량 강화
- 팀 내 지식 공유와 협업을 즐기는 **함께 성장하는 개발자**로 성장

---

<div align="center">

![footer](https://capsule-render.vercel.app/api?type=waving&color=gradient&height=150&section=footer)

</div>
