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
- 공지 서비스를 헥사고날 + MSA 고도화 
- 공통 페이징 유틸 설계 및 적용
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

- [생성] POST /api/notice/create
```
  → NoticeService.createNotice(NoticeCreateReq)
    1. dto.toEntity() → Notice 엔티티 생성
    2. NoticeJpaRepositoryVerify.createNotice() → Notice DB 저장 (CASCADE ALL)
```

- [수정] PATCH /api/notice/update/{id}
```
  → NoticeService.update()
    1. repository.findById(id) → 없으면 NoticeException(NOT_FOUND)
    2. null이 아닌 필드만 선택적 업데이트 (title / contents / author)
    3. repository.update(notice) → DB 저장
    반환: 업데이트된 NoticeDetailRes
```
- [조회] GET /api/notice/read/{id}
```
  → NoticeService.readDetails()
    1. repository.findById(id) → Notice 조회
    2. NoticeDetailRes.toDto(notice) → 응답
       (date: updatedAt 우선, 없으면 createdAt)
```
- [전체 조회] GET /api/notice/read/all
```
  → NoticeService.readList()
    1. repository.findAll() → Notice 목록 조회
       (없으면 NoticeException(NOT_FOUND))
    반환: NoticeInfoListRes
```
- [목록 조회 (페이징)] GET /api/notice/read/page/all
```
  → NoticeService.readList(pageable)
    1. repository.findAll(pageable) → Page<Notice> 조회
       (결과 없으면 NoticeException(NOTICE_NOT_FOUND))
    2. NoticeListResponse.toDtoPage(entityPage) → Page<NoticeListResponse> 변환
    반환: PageRes<NoticeListResponse> (currentPage·totalPages·totalElements·isFirst·isLast 포함)
```
- [삭제] DELETE /api/notice/delete/{id}
```
  → NoticeService.delete(id)
    1. repository.findById(id) → 없으면 NoticeException(NOT_FOUND)
    2. repository.delete(notice) → DB 삭제
    반환: "성공적으로 삭제 되었습니다."
```

### 프로모션 흐름 (모놀리식)

- [생성] POST /api/promotion/create  
```
  → PromotionService.createPromotion(PromotionCreateReq)
    1. couponRepository.findById(couponId)
       → Coupon 조회 (없으면 CouponException)
    2. dto.toEntity(coupon) → Promotion 엔티티 생성
       (coupon_id FK로 Coupon 객체 직접 연결)
    3. promotion.autoUpdateStatus() — 날짜 기반 자동 상태 결정
         now < startDate  → UPCOMING
         startDate ≤ now ≤ endDate  → ONGOING
         now > endDate  → ENDED
       (단, 이미 ENDED면 자동 갱신 건너뜀)
    4. repository.createPromotion() → DB 저장
```
- [수정] PATCH /api/promotion/update/{id}
```
  → PromotionService.update()
    1. repository.findById(id) → Promotion + 연결된 Coupon 조회
    2. null이 아닌 필드만 선택적 업데이트 (title / contents / startDate / endDate)
    3. 상태 처리:
         status == ENDED → promotion.updateStatus(ENDED) (수동 종료)
         else → promotion.autoUpdateStatus() (날짜 재계산)
    4. 쿠폰 변경 여부 판단:
         요청의 쿠폰 ID와 기존 쿠폰 ID가 다를 경우
         → couponRepository.findById(couponId) → promotion.updateCoupon(coupon)
    5. repository.update() → DB 저장
    반환: PromotionInfoRes (couponId · couponName · couponType 포함)
```
- [검색] GET /api/promotion/search
```
  → PromotionService.search()
    QueryDSL BooleanBuilder로 동적 조건 구성:
      keyword → title.contains(keyword).or(contents.contains(keyword))
      status  → promotion.status.eq(PromotionStatus)
    결과 PromotionInfoRes에 연결된 쿠폰 정보 함께 응답:
      couponType (PERCENTAGE / FIXED) · couponName · couponId
      (조건에 맞는 결과 없으면 빈 리스트 반환)
```
- [전체 조회] GET /api/promotion/read/all
```
  → PromotionService.readList()
    1. repository.findAll() → Promotion 목록 조회
       (없으면 PromotionException(NOT_FOUND))
    반환: PromotionInfoListRes
```
- [목록 조회 (페이징)] GET /api/promotion/read/page/all
```
  → PromotionService.readList(pageReq)
    1. repository.findAll(pageReq) → Page<Promotion> 조회
       (결과 없으면 PromotionException(NOT_FOUND))
    2. PromotionInfoRes.toDtoPage(entityPage) → Page<PromotionInfoRes> 변환
    반환: PageRes<PromotionInfoRes>
```
- [상세 조회] GET /api/promotion/read/{id}
```
  → PromotionService.readDetails(id)
    1. repository.findById(id) → Promotion + 연결된 Coupon 조회
       (없으면 PromotionException(NOT_FOUND))
    반환: PromotionInfoRes (couponId · couponName · couponType 포함)
```
- [삭제] DELETE /api/promotion/delete/{id}
```
  → PromotionService.delete(id)
    1. repository.findById(id) → 없으면 PromotionException(NOT_FOUND)
    2. repository.delete(promotion) → DB 삭제
    반환: "프로모션이 성공적으로 삭제 되었습니다."
```
- [상태 목록] GET /api/promotion/status
```
  → PromotionService.readStatus()
    1. PromotionStatus.values() → enum 전체 배열 [UPCOMING, ONGOING, ENDED] 반환
    2. stream()으로 순회하며 각 항목의 description(한글) 추출
         UPCOMING → "예정"
         ONGOING  → "진행중"
         ENDED    → "종료"
    3. 각 항목을 PromotionStatusInfoRes { description } DTO로 변환
    반환: PromotionStatusListRes (DB 접근 없음)
           promotionStatusInfos: ["예정", "진행중", "종료"] 고정값
```

### 공지사항 흐름 (MSA · 헥사고날) [구조확인](https://github.com/beyond-sw-camp/be17-fin-MeshX-HypeLink-BE/tree/Swagger/MSA/api-notice/src/main/java/com/example/apinotice/notice)

- [생성] POST /api/notice/create
```
  [ 인바운드 어댑터 (WebAdaptor) ]
    1. HTTP 요청 → NoticeSaveCommand 생성
    2. WebPort.create(command) 호출 (인터페이스 경계)
  [ UseCase (NoticeUseCase) ]
    3. NoticeMapper.toDomain(command) → Notice 도메인 모델 변환
    4. NoticePersistencePort.create(notice) 호출 (아웃바운드 포트 경계)
  [ 아웃바운드 어댑터 (NoticePersistenceAdaptor) ]
    5. NoticeMapper.toEntity(notice) → NoticeEntity 변환
    6. NoticeRepository.save(noticeEntity) (CASCADE ALL)
```
- [수정] PATCH /api/notice/update/{id}
```
  [ WebAdaptor ]
    1. NoticeUpdateCommand 수신 → WebPort.update(id, command) 호출
  [ NoticeUseCase ]
    2. noticePersistencePort.findById(id) → Notice 도메인 모델 조회
       (없으면 NoticeException(NOTICE_NOT_FOUND))
    3. null이 아닌 필드만 도메인 메서드로 업데이트:
         notice.updateTitle() / updateContents() / updateAuthor() 
    4. noticePersistencePort.update(notice) 호출
  [ NoticePersistenceAdaptor ]
    5. noticeRepository.findById(id) → NoticeEntity 조회
    6. entity.updateFields() → 필드 반영 후 save()
    반환: 도메인 모델 → NoticeInfoDto 변환 후 응답
```
- [조회] GET /api/notice/read/{id}
```
  [ WebAdaptor ]
    1. HTTP 요청 → id 파라미터 수신 → WebPort.read(id) 호출
  [ NoticeUseCase ]
    2. noticePersistencePort.findById(id) 호출 (아웃바운드 포트 경계)
  [ NoticePersistenceAdaptor ]
    3. noticeRepository.findById(id) → NoticeEntity 조회
       (없으면 NoticeException(NOTICE_NOT_FOUND))
    4. NoticeMapper.toDomain(entity) → Notice 도메인 모델 반환
  [ NoticeUseCase — 반환 처리 ]
    5. NoticeInfoDto.toDto(notice) → 응답
    반환: 도메인 모델 → NoticeInfoDto 변환 후 응답
       (date: updatedAt 우선, 없으면 createdAt)
```
- [전체 조회] GET /api/notice/read/all
```
  [ WebAdaptor ]
    1. HTTP 요청 → WebPort.readList() 호출
  [ NoticeUseCase ]
    2. noticePersistencePort.findAll() 호출 (아웃바운드 포트 경계)
  [ NoticePersistenceAdaptor ]
    3. noticeRepository.findAll() → NoticeEntity 목록 조회
    4. NoticeMapper.toDomain(entity) → Notice 도메인 모델 목록 변환
    반환: 도메인 모델 → NoticeListInfoDto 변환 후 응답
```
- [목록 조회 (페이징)] GET /api/notice/read/page/all
```
  [ WebAdaptor ]
    1. HTTP 요청 → Pageable 파라미터 수신 → WebPort.readList(pageable) 호출
  [ NoticeUseCase ]
    2. noticePersistencePort.findAll(pageable) 호출 (아웃바운드 포트 경계)
  [ NoticePersistenceAdaptor ]
    3. noticeRepository.findAll(pageable) → Page<NoticeEntity> 조회
    4. NoticeMapper.toDomain(entity) → Page<Notice> 변환
  [ NoticeUseCase — 반환 처리 ]
    5. NoticePageListInfoDto.toDtoPage(noticePage) → 도메인 → DTO 변환
    반환: PageRes<NoticePageListInfoDto> (currentPage·totalPages·totalElements·isFirst·isLast 포함)
```

---

## 🛠️ 기술 스택

**Backend** : Java 17, Spring Boot 3.5.6, Spring Security, Spring Data JPA, Spring WebSocket, Spring WebFlux,<br>Spring Retry + AOP, Spring Actuator, JWT (jjwt 0.11.5), QueryDSL 5.1.0, PortOne Server SDK 0.21.0,<br>Springdoc OpenAPI 2.8.4, Lombok

**CI/CD** : GitHub, Jenkins (K8s), Kaniko (executor:debug), Kubernetes, Gradle, DockerHub, Discord Webhook

![Java](https://img.shields.io/badge/Java_17-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot_3.5.6-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![Spring Security](https://img.shields.io/badge/Spring_Security-6DB33F?style=for-the-badge&logo=springsecurity&logoColor=white)
![Spring Data JPA](https://img.shields.io/badge/Spring_Data_JPA-6DB33F?style=for-the-badge&logo=spring&logoColor=white)
![Spring WebSocket](https://img.shields.io/badge/Spring_WebSocket-6DB33F?style=for-the-badge&logo=spring&logoColor=white)
![Spring WebFlux](https://img.shields.io/badge/Spring_WebFlux-6DB33F?style=for-the-badge&logo=spring&logoColor=white)
![JWT](https://img.shields.io/badge/JWT_0.11.5-black?style=for-the-badge&logo=jsonwebtokens&logoColor=white)
![QueryDSL](https://img.shields.io/badge/QueryDSL_5.1.0-0285C7?style=for-the-badge&logoColor=white)
![Swagger](https://img.shields.io/badge/Swagger_2.8.4-85EA2D?style=for-the-badge&logo=swagger&logoColor=black)
![Lombok](https://img.shields.io/badge/Lombok-red?style=for-the-badge&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=jenkins&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Gradle](https://img.shields.io/badge/Gradle-02303A?style=for-the-badge&logo=gradle&logoColor=white)
![DockerHub](https://img.shields.io/badge/DockerHub-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Discord](https://img.shields.io/badge/Discord_Webhook-5865F2?style=for-the-badge&logo=discord&logoColor=white)

---

## 🖥️ 모놀리식 아키텍처

<img width="7431" height="5973" alt="기존 시스템 아키텍처" src="https://github.com/user-attachments/assets/d20ef400-b831-4f31-bb95-94a1d519eaf9" />


---

## 🏗️ 마이크로서비스 아키텍처

<img width="9311" height="7528" alt="MSA 시스템 아키텍처" src="https://github.com/user-attachments/assets/d4c19c0a-2c47-4c2e-9f6b-98b3c7eea544" />


---

## 🤔 기술 선택 이유

<details>
<summary>Backend</summary>

| 선택 | 이유 |
|------|------|
| **MSA** | 기능별 서비스로 분리하여 독립 배포 및 장애 격리 실현 |
| **API Gateway** | 각 MSA로 요청을 동적으로 라우팅하여 클라이언트가 개별 서비스 주소를 알 필요 없음 |
| **Eureka** | 서비스 이름 기반 동적 라우팅 구현. API Gateway와 연동하여 인스턴스를 자동 탐색 |
| **Kafka** | 처리 시간이 긴 작업을 비동기 메시지로 처리하여 응답 속도 개선 및 서비스 간 결합도 감소 |
| **헥사고날 구조** | Domain이 외부 기술에 의존하지 않는 구조. 계층 분리로 외부 기술 교체 시 adapter만 수정 |
| **QueryDSL** | 복잡한 통계 쿼리에서 타입 안전 동적 쿼리 필요. JPQL 대비 컴파일 타임 오류 검출 가능 |

</details>

<details>
<summary>CI/CD</summary>

| 선택 | 이유 |
|------|------|
| **Kubernetes** | 물리 서버를 직접 클러스터로 구성하여 고가용성·확장성 확보 및 인프라 완전 제어 |
| **Jenkins** | 빌드마다 격리된 Pod 생성으로 환경 오염 없음. Gradle 캐시 볼륨 마운트로 반복 빌드 속도 개선 |
| **Ansible** | K8s 클러스터 구축·설정 자동화로 일관된 환경 구성 및 수작업 오류 제거 |
| **Kaniko** | K8s 환경에서 privileged 권한 없이 이미지 빌드 가능하여 DinD 대비 보안 위험 제거 |
| **Blue-Green 배포** | 배포 중 서비스 중단 없이 신버전으로 전환하고, 문제 발생 시 구버전으로 즉각 롤백 가능 |
| **GitHub Webhook** | main 브랜치 Push 시 Jenkins로 이벤트를 자동 전달하여 파이프라인을 즉시 트리거 |
| **Discord Webhook** | 빌드·배포 결과를 팀 채널에 자동 전송하여 배포 상태 실시간 공유 |

</details>

<details>
<summary>문서</summary>

| 선택 | 이유 |
|------|------|
| **Swagger** | Controller 어노테이션 기반으로 API 문서 자동 생성 → 코드와 문서 간 불일치 방지. 별도 문서 수동 관리 없이 Swagger UI로 즉시 테스트 가능 |
| **GitHub README / Wiki** | 코드 저장소와 문서를 한 곳에서 관리하여 버전 이력 추적 가능. Markdown 기반으로 아키텍처·흐름·트러블슈팅 등 구조화된 문서 작성 용이 |

</details>

---

## 🔑 핵심 구현 포인트

| 항목 | 위치 | 설명 |
|------|------|------|
| 공지사항<br> 관리 | `notice/service/NoticeService.java` | 공지 CRUD 전체 구현<br>수정 시 null이 아닌 필드만 선택<br>업데이트 불필요한 덮어쓰기 방지 |
| 페이징 | `common/PageReq.java`<br>`common/PageRes.java` | 공통 페이징 유틸 설계 및 적용<br>응답 구조 통일 |
| 프로모션<br>상태<br>자동화 | `promotion/model/entity/Promotion.java` | startDate/endDate 비교해<br> UPCOMING·ONGOING·ENDED<br> 자동 결정 관리자가 ENDED<br>한 경우 자동 갱신 제외 |
| 프로모션<br>쿠폰연결 | `promotion/service/PromotionService.java` | couponId로 조회 후 FK 연결<br>수정 요청 시 기존 ID와 비교해<br>변경된 경우에만 교체 |
| 프로모션<br>검색 | `promotion/repository/PromotionJpaRepositoryVerify.java` | QueryDSL로 키워드·상태 조건<br>동적 조합<br>조건 없는 항목은 쿼리 자동 제외되어<br>불필요한 전체 조회 방지 |
| 프로모션<br>상태목록 | `promotion/service/PromotionService.java` | `PromotionStatus.values()`로 enum<br> 전체 순회 후 한글 description 추출<br>DB 접근 없이 (예정·진행중·종료)을<br> DTO로 변환해 반환 |
| 헥사고날<br>구조 | `notice/usecase/port/NoticeUseCase.java`<br>`notice/adaptor/in/WebAdaptor.java`<br>`notice/adaptor/out/NoticePersistenceAdaptor.java` | WebAdaptor → UseCase →<br>PersistenceAdaptor 계층 분리<br>포트 인터페이스로 의존성 역전<br> 도메인 로직이 외부 기술에<br> 의존하지 않는 구조 설계 |
| 도메인<br>매퍼 | `notice/adaptor/out/mapper/NoticeMapper.java` | Entity·Command·Domain 간 변환을<br>Mapper 한 곳에 집중<br>레이어 경계에서 객체 변환 책임을<br> 명확히 분리해 의존성 오염 방지 |

### 주요 화면

<details>
<summary>📺 관리자 대시보드 화면 보기</summary>

#### 본사 로그인
![본사 관리자](https://github.com/user-attachments/assets/3d5406f6-9176-4b58-b819-286af2814787)

#### 고객 분석
![고객분석](https://github.com/user-attachments/assets/5c9d7b18-90b7-4ba4-a467-02744d73388d)

#### 전체 배송 추적
![전체배송추척](https://github.com/user-attachments/assets/dbcec5e0-5382-4e53-9e7b-87846d9f0b49)

#### AS 접수 처리
![AS](https://github.com/user-attachments/assets/1c9672ca-952e-4b9a-8f49-81fa4743d3b6)

</details>

<details>
<summary>💳 POS 단말기 화면 보기</summary>

#### POS 결제
![pos_gif](https://github.com/user-attachments/assets/086e6512-c76e-430a-8061-11aacb365e50)

#### 회원 결제
![포스기 회원 결제](https://github.com/user-attachments/assets/637100dd-1409-4bb3-90f7-d89f04595ca8)

#### 결제 내역
![포스기 결제내역](https://github.com/user-attachments/assets/7ee47852-b185-4ad7-8424-19bc6b10fbf1)

</details>

---

## 🔧 트러블슈팅 / 개선 경험

### Backend

- **프로모션 FK 설계 오류 — 폴리모픽 FK의 참조 무결성 위반** : 초기 설계에서 프로모션이 타입에 따라 옷·매장·카테고리 등 서로 다른 테이블을 가리키도록 구성되었습니다.
  한 컬럼이 상황에 따라 다른 테이블을 참조하는 폴리모픽 FK 구조는 DB가 참조 대상을 특정할 수 없어 FK 제약 조건 자체를 걸 수 없고, 참조 무결성을 보장하지 못한다는 것을 파악했습니다.
  FK는 반드시 단일 부모 테이블을 가리켜야 한다는 관계형 DB 원칙에 따라 프로모션의 참조 대상을 쿠폰 단일 엔티티로 재설계해 해결했습니다.
  이 경험으로 FK 설계 전 도메인 간 관계를 명확히 정의하지 않으면 DB 제약 조건 자체가 무너진다는 것을 체감했습니다.

- **페이징 처리 위치 수정** : 초기에는 프론트엔드에서 전체 데이터를 받아 클라이언트 단에서 페이징을 처리했으나, 데이터가 늘어날수록 불필요한 데이터 전송과 렌더링 부하가 커졌습니다.
  `Pageable`을 활용해 백엔드에서 페이징을 처리하고, `PageRes<T>` 공통 응답 구조를 설계하여 모든 목록 API에 일관되게 적용했습니다.
  페이징은 프론트가 아닌 백엔드에서 처리해야 네트워크 비용과 서버 부하를 함께 줄일 수 있다는 것을 깨달았습니다.

### CI/CD

- **Gradle 빌드 캐시 누락** : Jenkins Pod는 빌드마다 새로 생성되어 Gradle 의존성을 매번 처음부터 다운로드했고, 빌드 시간이 불필요하게 길었습니다.
  PVC(PersistentVolumeClaim)를 생성해 Gradle 캐시 디렉토리를 볼륨으로 마운트하고, Pod가 재생성되어도 캐시가 유지되도록 해결했습니다.
  컨테이너 기반 CI 환경에서는 Pod의 휘발성을 고려한 캐시 전략이 빌드 효율성과 직결된다는 것을 체감했습니다.

### 문서

- **Swagger 문서 자동화** : 이전 프로젝트에서 Swagger 어노테이션을 일일이 손수 작성하다 보니 API가 늘어날수록 문서화에만 상당한 시간이 소요됐습니다.
  이번 프로젝트에서는 AI 바이브코딩을 활용해 Controller 코드를 기반으로 `@Operation`, `@ApiResponse` 등 어노테이션을 자동 생성하는 방식으로 작업 속도를 높였습니다.
  반복적인 문서 작업에 AI를 보조 도구로 활용하면 핵심 로직 구현에 더 집중할 수 있다는 것을 체감했습니다.

- **기획서 자동화** : 기획서를 Word·PPT로 직접 작성하면 형식을 맞추는 데 시간이 많이 소요됐습니다.
  Typst에 작성한 코드를 입력하니 기획서가 자동으로 생성되어 문서 작업 시간을 크게 줄일 수 있었습니다.
  도구를 적절히 활용하면 반복적인 작업을 자동화하여 본래 목적에 집중할 수 있다는 것을 깨달았습니다.

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

필요 환경변수: `SPRING_DATASOURCE_URL`, `SPRING_DATASOURCE_USERNAME`, `SPRING_DATASOURCE_PASSWORD`, `SPRING_DATA_REDIS_HOST`, `SPRING_DATA_REDIS_PORT`, `JWT_SECRET`, `JWT_ACCESS_TOKEN_EXPIRATION_MS`, `JWT_REFRESH_TOKEN_EXPIRATION_MS`, `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_S3_BUCKET_NAME`, `PORTONE_STORE_ID`, `PORTONE_API_SECRET` 등

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

<details>
<summary>Swagger 보기</summary>

[direct_swagger.pdf](https://github.com/user-attachments/files/25679635/direct_swagger.pdf)

[auth_swagger.pdf](https://github.com/user-attachments/files/25679634/auth_swagger.pdf)

[notice_swagger.pdf](https://github.com/user-attachments/files/25679631/notice_swagger.pdf)

[item_swagger.pdf](https://github.com/user-attachments/files/25679630/item_swagger.pdf)

[Swagger.pdf](https://github.com/user-attachments/files/25679633/Swagger.pdf)

</details>

