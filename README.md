<div align="center">
  <img src="https://github.com/user-attachments/assets/807a5735-e104-4bbe-adf5-b7a47830b0cf" width="400"/>
</div>

## 한 줄 소개

실시간 배송 추적·재고 공유·권한 기반 중앙 관리를 통합한 B2B 직영점 운영 플랫폼

---

## 📋 프로젝트 개요

| 항목 | 내용 |
|------|------|
| **진행 기간** | 2025.10 ~ 2025.11 |
| **팀 인원** | 4명 |
| **내 역할** | 공지·프로모션 API 구현, MSA+헥사고널 고도화,  CI·CD 품질 검증, Swagger·README 문서화 |
| **핵심 기술** | Java, Spring Boot, JWT, Redis, PortOne, SpringDoc(Swagger), Kubernetes, Jenkins |

---

## 🕵️ 팀원 소개

<table align="center">
  <tbody>
    <tr>
      <td align="center"><a href="https://github.com/kbw07"><img src="https://github.com/user-attachments/assets/706e1875-8a3d-4d3e-9a19-d344d6866f23" width="100px;" alt=""/><br /><sub><b>강병욱</b></sub></a><br /></td>
      <td align="center"><a href="https://github.com/flionme"><img src="https://github.com/user-attachments/assets/08e896f8-c18f-454a-a44a-2337f585e77f" width="100px;" alt=""/><br /><sub><b>김성인</b></sub></a><br /></td>
      <td align="center"><a href="https://github.com/David9733"><img src="https://github.com/user-attachments/assets/4d6ad9a1-ac42-4f36-9259-2b988493cf85" width="100px;" alt=""/><br /><sub><b>이시욱</b></sub></a><br /></td>
      <td align="center"><a href="https://github.com/raccoon-coding"><img src="https://github.com/user-attachments/assets/90a33761-0bd8-4b73-a12a-1e24f0c5a6a9" width="100px;" alt=""/><br /><sub><b>최민성</b></sub></a><br /></td>
    </tr>
  </tbody>
</table>

---

## 🎯 프로젝트 목적

"데이터로 연결하고, 실시간으로 관리한다."

본사와 매장을 하나의 네트워크로 연결하여, 주문·재고·물류·매출·고객 데이터를 실시간으로 통합 관리하는<br>B2B 직영점 운영 솔루션입니다.

| 구분 | 기존 문제 | HypeLink 해결 | 기대 효과 |
|------|-----------|---------------|-----------|
| 재고 관리 | 점포별 분산, 본사 통합 불가 | POS 연동 실시간 재고 동기화 | 재고 손실 감소 |
| 물류 추적 | 배송 상태 실시간 파악 불가 | GPS 기반 기사 위치 추적 | 납기 지연 클레임 감소 |
| 고객 데이터 | POS·매장별 데이터 파편화 | 연령·구매패턴 통합 분석 | 맞춤 프로모션 가능 |
| 소통 채널 | 본사와 직영점 간 비효율 소통 | WebSocket 실시간 채팅 | 현장 대응력 강화 |

---

## 🙋 내 기여

### 1단계 · Backend

- **공지 API 구현**: 모놀리식 레이어드 구조에서 본사 공지 등록·조회·수정·삭제 API 설계 및 구현
- **프로모션 API 구현**: 모놀리식 레이어드 구조에서 프로모션 등록·조회·관리 API 설계 및 구현
- **공지 MSA 고도화**: 모놀리식 레이어드 구조의 공지 서비스를 마이크로서비스 헥사고날 구조로 직접 분리 및 고도화
- **지도 기능 조사 참여**: GPS 물류 추적 기능 구현을 위해 Naver Maps API 연동 방식 공동 조사 및 기술 검토

### 2단계 · CI/CD

- **파이프라인 품질 확인**: Jenkins + Kubernetes 배포 파이프라인 동작 검증 및 이슈 확인
- **동영상 시연 검토**: 배포 완료 후 시연 시나리오 확인 및 피드백

### 3단계 · 문서

- **Swagger API 명세 작성**: 담당 도메인(Notice·Promotion) API 명세 작성 및 전체 명세서 구조 정리
- **README 작성**: 프로젝트 전체 README 구성 및 작성
- **스프린트 위키**: [2차 스프린트 위키](https://github.com/beyond-sw-camp/be17-fin-MeshX-HypeLink-BE/wiki/Sprint-2) 정리

---

## ✨ 주요 기능

| 기능 | 설명 |
|------|------|
| 역할 기반 계정 관리 | 본사(ADMIN·MANAGER) / 매장(BRANCH_MANAGER) / POS / 배송기사 계정 분리 관리 |
| JWT + Redis 인증 | Access Token 블랙리스트 + Refresh Token 갱신으로 보안 로그아웃 구현 |
| PortOne 결제 검증 | 서버 측 금액 재검증 후 불일치 시 자동 취소, 영수증 및 재고 동시 처리 |
| 발주·재고 관리 | 본사↔매장 발주 흐름, 비관적 락으로 동시 접근 충돌 방지 |
| GPS 물류 추적 | 배송 기사 위치 실시간 수신 및 배송 상태 자동 전이 |
| 실시간 채팅 | WebSocket 기반 본사-직영점 실시간 메시지 채널 |
| 통계·분석 | QueryDSL 기반 매장별 매출·재고 집계 및 고객 패턴 분석 |
| 이미지 관리 | AWS S3 Presigned URL 기반 상품 이미지 업로드 |

---

## 🔄 사용자 흐름 (역할별)

| 역할 | 주요 흐름 |
|------|-----------|
| ADMIN / MANAGER | 직영점 계정 생성 → 상품 등록 → 발주 승인/반려 → 통계 조회 |
| BRANCH_MANAGER | 로그인 → 매장 재고 확인 → 발주 요청 → 배송 추적 → 실시간 채팅 |
| POS_MEMBER | POS 계정 로그인(코드 검증) → 상품 조회 → PortOne 결제 → 재고 자동 차감 |
| DRIVER | 로그인 → 배송 목록 확인 → GPS 위치 전송 → 배송 상태 업데이트 |

---

## 🌱 핵심 로직 흐름

### 인증 흐름

```
[클라이언트] 로그인 요청
  → AuthService.login(): 이메일/비밀번호 검증
  → JwtUtils.generateTokens(): Access Token + Refresh Token 발급
  → RedisTokenStore.saveRefreshToken(): Redis에 RT 저장 (key: "RT:{email}")
  → 응답: AccessToken (헤더) + RefreshToken (쿠키)

[토큰 갱신] RefreshToken 수신
  → RedisTokenStore.getRefreshToken(): Redis 저장값과 비교
  → 일치 시 새 토큰 발급

[로그아웃]
  → RefreshToken 삭제
  → AccessToken 남은 TTL만큼 블랙리스트 등록 (Redis key: AccessToken 값)
  → JwtAuthenticationFilter: 매 요청마다 블랙리스트 여부 확인
```

### 결제 검증 흐름

```
[POS] 결제 완료 후 paymentId 전송
  → PaymentService.validatePayment()
    1. PortOne 서버에서 실제 결제 정보 조회 (fetchAndValidatePortOnePayment)
    2. 결제 상태 검증 (PaidPayment 여부)
    3. 서버 계산 금액 vs PortOne 실제 금액 비교
    4. 불일치 시 → portOneService.cancelPayment() 자동 취소 + 예외 throw
    5. 일치 시 → 재고 차감 + 영수증 생성 + Payments 엔티티 저장
    6. 쿠폰 사용 처리 (customerCoupon.useCoupon())
```

### 발주 동시성 제어 흐름

```
[매장] 발주 승인 요청
  → PurchaseOrderService.update()
    1. 비관적 락 (PESSIMISTIC_WRITE) 으로 ItemDetail/StoreItemDetail 조회
    2. 재고 업데이트 (updateStock)
    3. LockTimeoutException / PessimisticLockException 발생 시
       → 최대 3회 재시도 (지연: 200ms × 시도 횟수)
    4. 3회 초과 시 BaseException throw
```

### CI/CD 파이프라인 흐름

```
[GitHub main 브랜치 push]
  → Jenkins WebHook 트리거
  → K8s Pod 생성 (gradle:8.9-jdk17 + kaniko 컨테이너)
  → Checkout (main branch)
  → Gradle Build: ./gradlew clean bootJar
  → Kaniko: Dockerfile 기반 이미지 빌드 → DockerHub push
      (raccoon98/hypelink-back:{BUILD_NUMBER}, :latest)
  → SSH → K8S_MASTER
      현재 Service selector 확인 (blue or green)
      → 비활성 색상 Deployment 배포 (replicas: 2)
      → kubectl rollout status 대기 (timeout 600s)
      → Service selector 전환 (ver: newColor)
      → 이전 Deployment replicas: 0 스케일다운
  → Discord Webhook 알림 (성공/실패)
```

---

## 🛠️ 기술 스택

### Backend

| 기술 | 버전 | 용도 |
|------|------|------|
| Java | 17 | 언어 |
| Spring Boot | 3.5.6 | 웹 프레임워크 |
| Spring Security | (Boot 관리) | 인증/인가 |
| Spring Data JPA | (Boot 관리) | ORM |
| Spring WebSocket | (Boot 관리) | 실시간 채팅 |
| Spring WebFlux | (Boot 관리) | 내부 HTTP 비동기 호출 (WebClient) |
| Spring Retry + AOP | (Boot 관리) | 재시도 정책 |
| Spring Actuator | (Boot 관리) | Health Check |
| JWT (jjwt) | 0.11.5 | 토큰 인증 |
| QueryDSL | 5.1.0 | 동적 쿼리 |
| PortOne Server SDK | 0.21.0 | 결제 검증 |
| Springdoc OpenAPI | 2.8.4 | Swagger UI |
| Lombok | (Boot 관리) | 보일러플레이트 제거 |

### Database / Infra

| 기술 | 버전 | 용도 |
|------|------|------|
| MariaDB | (입력 필요) | 관계형 DB |
| Redis | (Boot 관리) | Refresh Token 저장 / 블랙리스트 |
| AWS S3 (spring-cloud-aws) | 3.0.0 | 이미지 저장 |

### CI/CD / Infra

| 기술 | 버전/비고 | 용도 |
|------|-----------|------|
| Jenkins | (K8s 운영) | CI/CD 오케스트레이터 |
| Kaniko | gcr.io/kaniko-project/executor:debug | Docker 데몬 없는 이미지 빌드 |
| Kubernetes | (입력 필요) | 컨테이너 오케스트레이션 |
| Gradle | 8.9-jdk17 | 빌드 도구 |
| DockerHub | - | 이미지 레지스트리 |
| Discord Webhook | - | 빌드 알림 |

### Frontend

![Vue.js](https://img.shields.io/badge/vue.js-%2335495e.svg?style=for-the-badge&logo=vuedotjs&logoColor=%234FC08D)
![Pinia](https://img.shields.io/badge/Pinia-ffd859?style=for-the-badge&logoColor=black)
![Socket.js](https://img.shields.io/badge/Socket.io-black?style=for-the-badge&logo=socketdotio&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-323330?style=for-the-badge&logo=javascript&logoColor=F7DF1E)
![Axios](https://img.shields.io/badge/Axios-671ddf?style=for-the-badge&logo=axios&logoColor=white)

---

## 🖥️ 시스템 아키텍처

<img width="9311" height="7528" alt="MSA_" src="https://github.com/user-attachments/assets/3b30052e-3295-451b-85ab-cdb70c8d27d1" />

---

## 🏗️ CI/CD 아키텍처

> [CI/CD 파이프라인 상세 위키](https://github.com/beyond-sw-camp/be17-fin-MeshX-HypeLink-BE/wiki/HypeLink-CI-CD-%ED%8C%8C%EC%9D%B4%ED%94%84%EB%9D%BC%EC%9D%B8-%EB%AC%B8%EC%84%9C)

| 구분 | 흐름 | 배포 전략 |
|------|------|-----------|
| 트리거 | GitHub main 브랜치 push → Jenkins WebHook | - |
| 빌드 | K8s Pod (gradle:8.9-jdk17) → `./gradlew clean bootJar` | - |
| 이미지 | Kaniko → DockerHub (`raccoon98/hypelink-back:{BUILD_NUMBER}`) | 캐시 활성화 |
| 배포 | SSH → K8S_MASTER → kubectl apply | Blue-Green (무중단) |
| 검증 | startupProbe → livenessProbe → readinessProbe | 3단계 Health Check |
| 전환 | Service selector `ver: blue/green` 교체 → 구버전 replicas=0 | 즉시 트래픽 전환 |
| 알림 | Discord Webhook (성공/실패 Embed 메시지) | - |

```
GitHub Push
  └─► Jenkins (K8s Pod)
        ├─ gradle:8.9-jdk17  →  bootJar 빌드
        └─ kaniko             →  이미지 빌드 & DockerHub Push
              └─► SSH ► K8S Master
                    ├─ 현재 ver 확인 (blue/green)
                    ├─ 신규 Deployment 배포 (비활성 색상)
                    ├─ rollout status 대기
                    ├─ Service selector 전환
                    └─ 구버전 replicas=0
                          └─► Discord Webhook 알림
```

---

## 🤔 기술 선택 이유

<details>
<summary>Backend — Spring Boot / JWT+Redis / Spring Retry</summary>

**Spring Boot 3.5.6 + Java 17**
- LTS 버전 기반으로 안정성 확보
- Records, Sealed Classes 등 최신 언어 기능 활용 가능

**JWT + Redis 블랙리스트**
- Stateless 토큰으로 수평 확장(K8s 멀티 레플리카)에 적합
- 로그아웃 시 Access Token 즉시 무효화가 필요 → Redis TTL 기반 블랙리스트로 해결
- Refresh Token은 Redis에 저장하여 탈취 시 서버 측 삭제 가능

**PortOne Server SDK 0.21.0**
- 서버 측 결제 금액 재검증 필수 (클라이언트 금액 위변조 방지)
- SDK 제공 Cancel API로 검증 실패 시 자동 취소 원자성 구현

**Spring Retry + AOP**
- 비관적 락 경합 시 재시도를 별도 모듈로 분리하여 서비스 로직 오염 방지
- LockTimeoutException 발생 시 점진적 backoff (200ms × n회) 적용

**QueryDSL 5.1.0**
- 복잡한 통계 쿼리(매장별·기간별 매출, 재고 조회)에서 타입 안전 동적 쿼리 필요
- JPQL 문자열 방식 대비 컴파일 타임 오류 검출 가능

</details>

<details>
<summary>CI/CD — Kaniko / Blue-Green / Jenkins in K8s</summary>

**Kaniko (Docker 데몬 없는 빌드)**
- K8s 환경에서 privileged 권한 없이 컨테이너 내부 이미지 빌드 가능
- DinD(Docker-in-Docker) 대비 보안 위험 없음

**Blue-Green 배포 전략**
- 무중단 배포 필수: 매장 POS 결제 흐름 중 재시작 불가
- Service selector 전환으로 즉시 트래픽 절환, 이슈 발생 시 이전 색상으로 롤백 가능

**Jenkins in Kubernetes**
- 빌드마다 격리된 Pod 생성 → 빌드 간 환경 오염 없음
- Gradle 캐시 볼륨 마운트로 반복 빌드 속도 개선

**Discord Webhook 알림**
- 팀 협업 채널에 빌드 결과 자동 전송 → 배포 상태 실시간 공유

</details>

<details>
<summary>Infra — MariaDB / Redis / AWS S3</summary>

**MariaDB**
- MySQL 호환 오픈소스 RDBMS로 K8s 환경 배포 용이
- 트랜잭션 안정성 필요한 재고·결제·발주 도메인에 적합

**Redis**
- Token Store, 블랙리스트 모두 TTL 기반 자동 만료 지원
- 인메모리 조회로 매 요청마다 발생하는 토큰 검증 지연 최소화

**AWS S3 + Presigned URL**
- 대용량 상품 이미지를 서버 경유 없이 클라이언트가 직접 업로드
- 서버 부하 감소 및 업로드 속도 개선

</details>

---

## 🔑 핵심 메서드 (대표 파트)

| 메서드 | 위치 | 설명 |
|--------|------|------|
| `register()` | `auth/service/AuthService.java` | 역할별 계정 생성 분기 (POS 코드 검증, 매장 등록 시 지오코딩 포함) |
| `login()` | `auth/service/AuthService.java` | 비밀번호 검증 + Access/Refresh Token 발급 |
| `logout()` | `auth/service/AuthService.java` | RT 삭제 + AT 블랙리스트 등록 (잔여 TTL 기준) |
| `blacklistToken()` | `auth/service/RedisTokenStore.java` | Redis에 AccessToken을 잔여 만료시간만큼 저장 |
| `validatePayment()` | `direct_store/payment/service/PaymentService.java` | PortOne 실제 결제 조회 → 금액 검증 → 실패 시 자동 취소 |
| `createReceiptAndPayment()` | `direct_store/payment/service/PaymentService.java` | 재고 차감 + 영수증 생성 + Payments 저장 동일 트랜잭션 처리 |
| `update()` | `head_office/order/service/PurchaseOrderService.java` | 비관적 락 + 최대 3회 재시도 (200ms × n backoff) 발주 승인 |
| `connecting()` | `head_office/shipment/service/ShipmentService.java` | 배송 기사 배정 + ShipmentStatus.DRIVER_ASSIGNED 상태 전이 |

---

## 🔧 트러블슈팅 / 개선 경험

### [Backend] 발주 동시성 충돌 — 비관적 락 + 재시도 로직

**문제**: 복수 매장이 동시에 동일 상품 재고에 발주를 요청할 때 재고 음수 현상 발생 가능성<br>
**원인**: 낙관적 락만으로는 충돌 시 예외 처리 후 재시도 로직 구현이 복잡<br>
**해결**: `PESSIMISTIC_WRITE` 락으로 ItemDetail 조회 → `LockTimeoutException` 발생 시 최대 3회 재시도 (200ms × 시도 횟수 backoff) 적용<br>
**결과**: 동시 발주 충돌 시 자동 재시도로 대부분 처리 가능, 3회 초과 시 명시적 예외 반환 (측정 필요)

### [Backend] 결제 검증 실패 시 부분 상태 불일치

**문제**: PortOne 결제는 성공했으나 금액 불일치 또는 재고 부족 시 결제 취소 처리 누락 위험<br>
**원인**: 결제 검증과 재고/영수증 처리가 별도 단계로 분리되어 중간 실패 시 취소 누락<br>
**해결**: `validatePayment()` 전체를 try-catch로 감싸 어떤 예외든 `portOneService.cancelPayment()` 먼저 호출 후 예외 re-throw<br>
**결과**: 결제 취소 누락 없이 클라이언트에 명확한 오류 반환 (측정 필요)

### [Backend] 로그아웃 후 Access Token 재사용 가능 문제

**문제**: JWT는 Stateless이므로 로그아웃 후에도 만료 전 Access Token이 유효<br>
**원인**: JWT 자체를 서버에서 무효화하는 표준 방법 없음<br>
**해결**: 로그아웃 시 Access Token의 잔여 TTL을 계산 → Redis에 해당 토큰을 key로 `"logout"` 저장. `JwtAuthenticationFilter`에서 매 요청마다 `isBlacklisted()` 체크<br>
**결과**: 로그아웃 후 AT 재사용 방지 (Redis 조회 1회 추가, 측정 필요)

### [CI/CD] Docker 빌드 권한 문제 — Kaniko 도입

**문제**: K8s 파이프라인에서 DinD 방식으로 Docker 이미지 빌드 시 `privileged` 권한 필요<br>
**원인**: K8s 보안 정책상 privileged 컨테이너 실행 제한<br>
**해결**: Kaniko(`gcr.io/kaniko-project/executor:debug`)로 교체 → privileged 없이 컨테이너 내부 이미지 빌드<br>
**결과**: 보안 컨텍스트 제한 환경에서 정상 빌드·Push 가능

### [CI/CD] 무중단 배포 — Blue-Green 전략 구현

**문제**: 배포 중 재시작으로 인해 매장 POS 결제 흐름이 끊기는 위험<br>
**원인**: Rolling Update 방식에서도 파드 교체 시 일시적 연결 끊김 발생 가능<br>
**해결**: Blue-Green 배포 스크립트를 Jenkinsfile에 직접 구현. 현재 활성 색상 감지 → 비활성 Deployment 신규 배포 → `rollout status` 대기 → Service selector 전환 → 구버전 replicas=0<br>
**결과**: 트래픽 전환 시 다운타임 없이 신규 버전 전환 (측정 필요)

---

## 🚀 실행 및 테스트

### 로컬 실행

```bash
# 1. 빌드
./gradlew clean bootJar

# 2. 실행 (환경변수 설정 후)
java -jar build/libs/*.jar
```

### Docker 실행

```bash
docker build -t hypelink-back .
docker run -p 8080:8080 \
  -e SPRING_DATASOURCE_URL=... \
  hypelink-back
```

### 필수 환경변수 (키 목록)

```
SPRING_DATASOURCE_URL
SPRING_DATASOURCE_USERNAME
SPRING_DATASOURCE_PASSWORD
SPRING_DATA_REDIS_HOST
SPRING_DATA_REDIS_PORT
JWT_SECRET
JWT_ACCESS_TOKEN_EXPIRATION_MS
JWT_REFRESH_TOKEN_EXPIRATION_MS
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_S3_BUCKET_NAME
PORTONE_STORE_ID
PORTONE_API_SECRET
```

### Swagger UI

```
http://localhost:8080/swagger-ui/index.html
```

### CI/CD 파이프라인 트리거

```bash
# main 브랜치 push 시 Jenkins WebHook 자동 실행
git push origin main

# K8s 배포 상태 확인
kubectl get pods -n hypelink
kubectl get service hypelink-svc -n hypelink
```

---

## 📎 참고자료

| 자료 | 링크 |
|------|------|
| CI/CD 파이프라인 위키 | [바로가기](https://github.com/beyond-sw-camp/be17-fin-MeshX-HypeLink-BE/wiki/HypeLink-CI-CD-%ED%8C%8C%EC%9D%B4%ED%94%84%EB%9D%BC%EC%9D%B8-%EB%AC%B8%EC%84%9C) |
| 2차 스프린트 위키 | [바로가기](https://github.com/beyond-sw-camp/be17-fin-MeshX-HypeLink-BE/wiki/Sprint-2) |
| Swagger UI (배포 환경) | [바로가기](https://www.meshx.store/swagger-ui/index.html) |
| Auth API 명세서 (PDF) | [열기](./doc/swagger/auth_swagger.pdf) |
| Direct API 명세서 (PDF) | [열기](./doc/swagger/direct_swagger.pdf) |
| Item API 명세서 (PDF) | [열기](./doc/swagger/item_swagger.pdf) |
| Notice API 명세서 (PDF) | [열기](./doc/swagger/notice_swagger.pdf) |
| ERD (본사 통합 + 모듈별) | 아래 펼치기 참조 |
| 프론트엔드 레포 | [바로가기](https://github.com/beyond-sw-camp/be17-fin-MeshX-HypeLink-FE) |
| 기획서 (PDF) | [열기](./doc/HypeLink%20기획서.pdf) |
| 요구사항 정의서 (PDF) | [열기](./doc/HypeLink%20요구사항%20정의서.pdf) |
| WBS (PDF) | [열기](./doc/WBS.pdf) |

<details>
<summary>본사 ERD 펼치기/접기</summary>
<div markdown="1">

## 본사 ERD
<img width="6098" height="6796" alt="hypelinkERD" src="https://github.com/user-attachments/assets/5d69fadd-c449-4fd8-a777-5474397b4937" />

</div>
</details>

<details>
<summary>MSA 모듈 ERD 펼치기/접기</summary>
<div markdown="1">

## AUTH ERD
<img width="2664" height="1490" alt="authERD" src="https://github.com/user-attachments/assets/b1261ca8-2706-40ed-868b-42c8a4723a02" />

## DIRECT ERD
<img width="3018" height="3112" alt="directERD" src="https://github.com/user-attachments/assets/5759509a-76b8-4e68-9d93-7b0306c95a50" />

## ITEM ERD
<img width="1958" height="1812" alt="itemERD" src="https://github.com/user-attachments/assets/d6dcd56f-36fb-46bb-a57d-ab3d71c09f15" />

## NOTICE ERD
<img width="840" height="1100" alt="noticeERD" src="https://github.com/user-attachments/assets/bd19f0e2-4b48-421d-8036-fa9ff830c375" />

</div>
</details>
