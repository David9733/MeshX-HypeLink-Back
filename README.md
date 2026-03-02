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

- 공지 CRUD API 설계 및 구현
- 프로모션 CRUD API 설계 및 구현
- 공지 서비스를 헥사고날 + MSA 고도화 [(MSA 구조확인)](https://github.com/beyond-sw-camp/be17-fin-MeshX-HypeLink-BE/tree/Swagger/MSA/api-notice/src/main/java/com/example/apinotice/notice)
- Naver Maps API 연동 방식 조사 및 기술 검토

### 2단계 · CI/CD

- Jenkins + Kubernetes 동작 검증 및 이슈 확인
- 시연 시나리오 확인 및 피드백

### 3단계 · 문서

- SpringDoc(Swagger) 기반 API 문서화 적용
- 프로젝트 전체 README 구성 및 작성
- 기획서 작성 및 위키, 발표 자료 개선

---

## ✨ 주요 기능

- GPS 실시간 추적 및 매장 도착 예상 시간 제공
- 매장별 POS 상태 조회 및 고장 접수·처리 상태 추적
- 연령·성별·카테고리별 고객 매출 분석 및 인기상품 랭킹
- 본사와 가맹점 재고 실시간 동기화 및 발주
- 본사와 가맹점 실시간 메신저 및 공지 전달
- 쿠폰 생성·관리 및 프로모션 등록·조회

---

## 👥 역할별 권한

| 역할 | 접근 범위 |
|------|---------|
| **본사** | 서브관리자 기능 전체 포함 + 계정·권한 관리 |
| **서브관리자** | 전체 매장 현황 조회, 발주 승인, 배송 기사 배정, GPS 배송 추적, POS 상태 점검, 고객·매출 분석,<br> 재고 및 상품 관리, 프로모션·쿠폰 생성·관리, 공지 발송, 메신저, AS 처리 |
| **가맹점** | 내 매장 재고 조회 및 매출 조회, 발주 요청, AS 신청, 메신저, 프로모션·공지 조회 |
| **POS기** | 상품 선택·결제(일반/카드/회원), 결제 내역 조회, 공지 조회 |

---

## 🌱 핵심 로직 흐름

### 공지사항 흐름 (모놀리식)

코드 근거: `src/main/java/.../head_office/notice/`

```
[생성] POST /api/notice/create
  → NoticeService.createNotice(NoticeCreateReq)
    1. dto.toEntity() → Notice 엔티티 생성 (isOpen 기본값: false)
    2. ImageService로 이미지 S3 저장 → Image 엔티티 반환
    3. 각 Image → NoticeImages 생성 후 notice.addNoticeImage() 연결
    4. NoticeJpaRepositoryVerify.createNotice() → DB 저장

[수정] PATCH /api/notice/update/{id}
  → NoticeService.update()
    1. repository.findById(id) → 없으면 NoticeException(NOT_FOUND)
    2. null이 아닌 필드만 선택적 업데이트 (title / contents / author)
    3. 이미지 교체: notice.clearImages() → 새 이미지 재연결
    4. repository.update(notice) → DB 저장
    반환: 업데이트된 NoticeDetailRes (S3 URL 포함)

[조회] GET /api/notice/read/{id}
  → NoticeService.readDetails()
    1. repository.findById(id) → Notice 조회
    2. exportS3Url(image) 함수로 S3 키 → 공개 URL 변환
    3. NoticeDetailRes.toDto(notice, urlGenerator) → 응답
       (date: updatedAt 우선, 없으면 createdAt)
```

### 프로모션 흐름 (모놀리식) — Coupon 연동 포함

코드 근거: `src/main/java/.../head_office/promotion/` + `.../coupon/`

```
[생성] POST /api/promotion/create  (@PreAuthorize ADMIN·MANAGER)
  → PromotionService.createPromotion(PromotionCreateReq)
    1. couponRepository.findById(couponId)
       → Coupon 조회 (없으면 CouponException)
    2. dto.toEntity(coupon) → Promotion 엔티티 생성
       (coupon_id FK로 Coupon 객체 직접 연결)
    3. ImageService로 이미지 S3 저장
    4. 각 Image → PromotionImages 생성 후 연결
    5. promotion.autoUpdateStatus() — 날짜 기반 자동 상태 결정
         now < startDate  → UPCOMING
         startDate ≤ now ≤ endDate  → ONGOING
         now > endDate  → ENDED
       (단, 이미 ENDED면 자동 갱신 건너뜀)
    6. repository.createPromotion() → DB 저장

[수정] PATCH /api/promotion/update/{id}
  → PromotionService.update()
    1. repository.findById(id) → Promotion + 연결된 Coupon 조회
    2. 쿠폰 변경 여부 판단:
         couponId != promotion.getCoupon().getId()
         → couponRepository.findById(newCouponId)
         → promotion.updateCoupon(newCoupon)
    3. 상태 처리:
         status == ENDED → promotion.updateStatus(ENDED) (수동 종료)
         else → promotion.autoUpdateStatus() (날짜 재계산)
    4. 이미지 교체 + repository.update() → DB 저장
    반환: PromotionInfoRes (couponId · couponName · couponType 포함)

[검색] GET /api/promotion/search?keyword=세일&status=진행중
  → PromotionService.search()
    QueryDSL BooleanBuilder로 동적 조건 구성:
      keyword → title.contains(keyword).or(contents.contains(keyword))
      status  → promotion.status.eq(PromotionStatus)
    결과 PromotionInfoRes에 연결된 쿠폰 정보 함께 응답:
      couponType (PERCENTAGE / FIXED) · couponName · couponId
```

### 공지사항 흐름 (MSA · 헥사고날) — api-notice 기준

코드 근거: `api-notice/src/main/java/com/example/apinotice/notice/`

헥사고날 레이어 구조:
```
외부 HTTP → [인바운드 어댑터] → (WebPort) → [UseCase] → (NoticePersistencePort) → [아웃바운드 어댑터] → DB
             WebAdaptor                    NoticeUseCase                          NoticePersistenceAdaptor
```

```
[생성] POST /api/notice/create
  ── 인바운드 어댑터 (WebAdaptor) ──
    1. HTTP 요청 → NoticeSaveCommand 생성
    2. WebPort.create(command) 호출 (인터페이스 경계)
  ── UseCase (NoticeUseCase) ──
    3. NoticeMapper.toDomain(command) → Notice 도메인 모델 변환
       (isOpen 기본값 false 설정)
    4. NoticePersistencePort.create(notice) 호출 (아웃바운드 포트 경계)
  ── 아웃바운드 어댑터 (NoticePersistenceAdaptor) ──
    5. NoticeMapper.toEntity(notice) → NoticeEntity 변환
    6. 각 NoticeImage → NoticeImageEntity 생성
       noticeEntity.addImageEntity(imgEntity) — 양방향 관계 설정
    7. NoticeRepository.save(noticeEntity)
       (CASCADE ALL → NoticeImageEntity 함께 저장)

[수정] PATCH /api/notice/update/{id}
  ── WebAdaptor ──
    1. NoticeUpdateCommand 수신 → WebPort.update(id, command) 호출
  ── NoticeUseCase ──
    2. noticePersistencePort.findById(id) → Notice 도메인 모델 조회
       (없으면 NoticeException(NOTICE_NOT_FOUND))
    3. null이 아닌 필드만 도메인 메서드로 업데이트:
         notice.updateTitle() / updateContents() / updateAuthor()
    4. notice.clearImages() → 새 이미지 목록 설정
    5. noticePersistencePort.update(notice) 호출
  ── NoticePersistenceAdaptor ──
    6. noticeRepository.findById(id) → NoticeEntity 조회
    7. entity.updateFields() — 필드 반영
    8. entity.clearImages() — orphanRemoval로 기존 이미지 자동 삭제
    9. 새 NoticeImageEntity 추가 후 save()
    반환: 도메인 모델 → NoticeInfoDto 변환 후 응답

[의존성 역전 — 핵심 원칙]
  도메인(Notice)은 DB·HTTP를 전혀 모름
  UseCase는 인터페이스(Port)에만 의존 → 구현체 교체 가능
  Mapper가 도메인 ↔ 엔티티 ↔ Command 간 변환 전담
  Eureka 서비스 디스커버리 자동 등록 (MSA Pod IP 기반)
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

## 🖥️ 모놀리식 아키텍처

<img width="6538" height="3727" alt="시스템 아키텍처" src="https://github.com/user-attachments/assets/c5fa309f-8215-4d9a-b35e-9becdbaea2e5" />

---

## 🏗️ 마이크로서비스 아키텍처

<img width="9492" height="7614" alt="MSA 시스템 아키텍처 " src="https://github.com/user-attachments/assets/fc798436-09e6-4cff-b0d7-c7448875f925" />


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

[기획서 보기](https://github.com/user-attachments/files/25619989/HypeLink.pdf)

[발표 PPT 보기](https://github.com/user-attachments/files/25619993/meshX.PPT.pdf)

