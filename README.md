# 최정환 | Backend Developer

Java / Spring 기반 백엔드 개발자를 목표로 공부하고 있습니다.

- 기능 구현에서 끝내지 않고, **동시성 · 트랜잭션 · 성능 문제를 직접 재현하고 측정해서** 해결하는 것을 중요하게 생각합니다.
- 기술을 도입하기 전에 "정말 필요한가"를 먼저 측정하고, 선택한 이유와 포기한 것을 함께 기록합니다.
- NHN Academy 백엔드 과정에서 MSA 기반 팀 프로젝트를 경험했습니다.

<br/>

## Tech Stack

| 분류 | 기술 |
|---|---|
| Language | Java 21 |
| Framework | Spring Boot, Spring Security, Spring Data JPA, Spring Cloud Gateway |
| Database | MySQL, PostgreSQL (pgvector) |
| Messaging / Cache | Kafka, RabbitMQ, Redis (Redisson) |
| Infra / Test | Docker Compose, JUnit5, Mockito, K6 |
| Frontend | React, Next.js, TypeScript |

<br/>

## Projects

### DocuMind — PDF 문서 기반 질의응답 서비스 (RAG)

`개인 프로젝트` · Spring Boot, Spring AI, PostgreSQL + pgvector, Flyway, Next.js
· [Repository](https://github.com/JJungH0/documind)

LLM 호출 자체보다, 그 앞뒤의 백엔드(문서 처리, 벡터 검색, 트랜잭션 경계, 외부 API 장애 대응)에 집중했습니다.

| 문제 | 해결 | 결과 |
|---|---|---|
| 큰 PDF 업로드 시 요청이 처리 완료까지 붙잡힘 | 전용 스레드 풀로 비동기 처리, job 번호만 즉시 응답 | 응답 **5.29s → 0.017s** |
| 외부 API 응답을 기다리는 동안 DB 커넥션 점유 | API 호출은 트랜잭션 밖에서, 저장만 짧은 트랜잭션으로 분리 | 대기 중 커넥션 미사용 |
| OpenAI 실패 시 처음부터 다시 처리 | 실패 원인 분류, 배치 단위 재시도, 남은 청크부터 이어서 처리 | 중복 토큰 0, 처리 **5.5s → 1.4s** |
| 청크를 한 건씩 INSERT | 청크 테이블만 SEQUENCE 전략으로 변경 후 JDBC 배치 적용 | 1,082건을 **배치 22회**로 저장 |
| 데이터가 늘수록 벡터 검색이 느려짐 | HNSW 인덱스 적용, 재현율을 측정해 설정값 결정 | 청크 5만 개 **280ms → 0.3ms** |

- 시맨틱 캐싱은 구현 전에 질문 쌍의 유사도를 먼저 측정했고, 답이 다른 질문이 더 비슷하게 나와 **도입하지 않기로 결정**했습니다.

<br/>

### ShopFlow — MSA 기반 이커머스 백엔드

`개인 프로젝트` · Spring Boot, Spring Cloud Gateway, Kafka, Redis(Redisson), MySQL, K6
· [Repository](https://github.com/JJungH0/shopflow)

동시 주문 상황의 재고 정합성과, 서비스 간 비동기 통신에서 생기는 문제를 다뤘습니다.

| 문제 | 해결 | 결과 |
|---|---|---|
| 동시 주문 시 재고 불일치 | 낙관적 락 / 비관적 락 / Redis 스핀 락 / Redisson 4가지를 구현해 동일 조건에서 측정 | 100건 중 11건 성공 → **100건 모두 성공** |
| 서비스별 DB 분리로 트랜잭션을 묶을 수 없음 | Kafka 기반 Saga 패턴 + 보상 트랜잭션 | 재고 부족 시 주문 자동 취소 |
| DB 저장과 이벤트 발행의 원자성 부재 | Outbox 패턴으로 이벤트를 DB에 먼저 저장 | Kafka 장애 중 접수된 주문도 **복구 시 자동 발행** |
| 상품 목록 조회 응답 지연 | Redis 캐싱 적용 후 K6로 효과 검증 | 평균 응답 **52.9ms → 27.7ms** |

- 측정상 가장 빠른 방식은 비관적 락(151ms)이었지만, 락 대기 중 DB 커넥션을 점유해 **커넥션 풀이 먼저 고갈될 수 있고** 다중 인스턴스 확장에 불리하다고 판단해 Redisson 분산 락(462ms)을 선택했습니다.
- 락 획득/해제와 트랜잭션 경계를 분리해, 커밋 전에 락이 풀려 갱신 전 데이터를 읽는 문제를 막았습니다.

<br/>

### Book1lluwa — 온라인 도서 쇼핑몰 (MSA)

`팀 프로젝트 · NHN Academy` · 2025.06 ~ 2025.07 · **쿠폰/이벤트 도메인 담당**
· Spring Boot, Spring Cloud, RabbitMQ, MySQL
· [Organization](https://github.com/nhnacademy-be10-1lluwa) · [서비스](https://book1lluwa.store) · [API 명세](https://book1lluwa.store/docs.html) · [소개 영상](https://youtu.be/Mm8H87yzw7I)

| 문제 | 해결 | 결과 |
|---|---|---|
| 회원가입·결제 시 쿠폰을 동기 발급해 API 응답 지연·실패 | RabbitMQ 기반 비동기 발급으로 전환 | 쿠폰 발급이 회원가입·결제 응답에 영향을 주지 않음 |
| 쿠폰 관련 장애 원인 추적이 어려움 | 발급/사용/만료/취소 상태 전이를 모두 이력으로 기록 | 문제 재현과 원인 추적 가능 |

- 쿠폰 정책(발급/사용/만료/취소) 설계 및 CRUD, Spring Scheduler 기반 생일 쿠폰 자동 발급을 구현했습니다.

<br/>

### 그 밖의 프로젝트

| 프로젝트 | 내용 |
|---|---|
| [url-project](https://github.com/JJungH0/url-project) | URL 단축 서비스 — JWT(Access/Refresh Token), Redis 기반 API별 Rate Limiting |
| [simple-cms-api](https://github.com/JJungH0/simple-cms-api) | Spring Security 세션 인증, Role 기반 권한 처리 CMS REST API |
| [dash-board](https://github.com/JJungH0/dash-board) | Next.js App Router 대시보드 ([배포](https://jjung-dashboard.vercel.app/)) |

<br/>

## Study

Spring 핵심 원리부터 MVC, JPA까지 단계별로 실습하고 정리했습니다.

[SpringCore](https://github.com/JJungH0/SpringCore) ·
[Spring MVC](https://github.com/JJungH0?tab=repositories&q=Spring-MVC) ·
[Spring JPA](https://github.com/JJungH0/Spring-JPA) ·
[Spring Data JPA](https://github.com/JJungH0/Spring-Data-JPA) ·
[Servlet / JSP](https://github.com/JJungH0/Servlet-Jsp) ·
[Notion](https://bottlenose-balloon-0b4.notion.site/1b95c23e942f8197948befcbec5a50f4?v=1b95c23e942f8121b0e2000c57156735&source=copy_link)
