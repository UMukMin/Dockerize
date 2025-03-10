# 타베로그(UMukMin) RPD (Product Requirements Document)

## 1. 개요(Overview)

**타베로그(UMukMin)**은 사용자가 음식점 리뷰를 작성하고, 다른 사용자의 리뷰를 열람할 수 있는 웹 서비스입니다. React.js + Next.js(프론트엔드)와 Django REST Framework(백엔드)를 사용해 구성하며, Google Maps API를 연동하여 지도를 통한 위치 정보와 리뷰를 함께 제공하는 것이 주요 목표입니다.

본 RPD는 서비스 개발을 위한 **구체적인 요구 사항**, **설계 방향**, **일정** 및 **리소스**를 정의합니다. 특히 데이터베이스는 **MySQL**(관계형)과 **MongoDB**(NoSQL)를 함께 고려하여, 프로젝트 요구 사항에 최적화된 방식으로 데이터를 관리할 수 있도록 합니다.

---

## 2. 목표(Objectives)

1. **사용자 친화적 인터페이스**를 제공하여 직관적인 리뷰 작성 및 열람 기능을 구현한다.  
2. **지도 API 연동**을 통해 음식점 위치를 표시하고, 직관적으로 식당을 찾고 리뷰를 확인할 수 있게 한다.  
3. **CRUD**(Create, Read, Update, Delete) 기능을 확실하게 구현하여 사용자의 리뷰 작성/관리 및 수정/삭제가 가능하도록 한다.  
4. **평가(별점) 기능**을 제공하여 음식점별 평점을 시각적으로 표현하고, 평균 평점을 확인할 수 있도록 한다.  
5. **유연한 데이터베이스 아키텍처**(MySQL + MongoDB 병행 가능)를 적용하여 확장성과 유지보수성을 높인다.

---

## 3. 기능 요구사항(Features)

### 3.1 사용자 인증(User Authentication)
- **회원가입, 로그인, 로그아웃** 기능
- **비밀번호 분실 시 재설정** 가능
- JWT 기반 인증 및 세션 관리
- (선택 사항) 소셜 로그인

### 3.2 리뷰(Reviews)
- 리뷰 **CRUD** 기능  
  - **Create**: 식당을 선택 후 리뷰 작성(별점 1~3, 텍스트, 사진(Optional))  
  - **Read**: 특정 식당에 대한 리뷰 목록 조회  
  - **Update**: 본인이 작성한 리뷰만 수정 가능  
  - **Delete**: 본인이 작성한 리뷰만 삭제 가능
- 리뷰 상세 페이지에 **평균 별점** 및 **리뷰 개수** 표시
- 리뷰에 **작성자 닉네임, 작성 날짜, 수정 날짜(자동 갱신)** 표시

### 3.3 지도(Map Integration)
- **Google Maps JavaScript API** 연동  
- 지도에 **식당 위치** 마커 표시  
- 마커 클릭 시 **식당 정보(이름, 주소, 평균 평점 등) 및 리뷰 페이지 링크** 제공  
- **식당 검색**(이름/위치 기반) 기능  
- (선택 사항) 위치 기반 **주변 식당 탐색** 기능

### 3.4 별점(Rating System)
- 1~3점(별)으로 구성된 **단일 평점 시스템**  
- 식당별 평균 평점 및 리뷰 수 표시  
- (추후) 별점 범위 확장 검토 가능(예: 1~5점)

### 3.5 유저 프로필 관리 (추후 Beta에 반영)
- 프로필 사진 업로드
- 닉네임/자기소개 수정
- 내가 작성한 리뷰 목록 조회

### 3.6 검색 및 필터(추후 Beta에 반영)
- 음식점 이름, 위치, 카테고리(한식, 중식, 일식 등) 등을 기반으로 검색
- 별점, 리뷰 개수 등을 활용한 필터링

---

## 4. 기술 스택(Technical Stack)

### 4.1 프론트엔드(Frontend)
- **React.js + Next.js**
  - 서버 사이드 렌더링(SSR) 지원
  - TypeScript 사용
  - 라우팅: Next.js 내장 라우팅
- **스타일링**: TailwindCSS
  - 반응형 디자인 구현
  - 커스텀 테마 설정 가능
- **HTTP Client**: Axios
- **상태관리**: React Hooks + Context API(필요 시 Redux 고려)

### 4.2 백엔드(Backend)
- **Django 3.2+** (LTS 버전 고려)  
- **Django REST Framework(DRF)**  
  - RESTful API 설계
  - ViewSet, Serializers, Permissions, Throttling
  - Swagger/OpenAPI 문서 자동화
- **인증**: JWT 토큰 인증
  - djangorestframework-simplejwt 또는 커스텀 JWT 인증

### 4.3 맵 API(Map API)
- **Google Maps JavaScript API**
  - 지도 표시, 마커 표시, 식당 정보 표시
  - (옵션) Directions, Places API 등 추가 기능은 추후 필요 시 고려

### 4.4 데이터베이스(Database)
#### 4.4.1 MySQL
- **MySQL 8.0+**  
  - 관계형 스키마 설계  
  - 트랜잭션 관리  
  - InnoDB 엔진 사용 권장  
  - Django ORM과 궁합이 좋아, 사용자/리뷰 등 **정형화된 데이터** 관리에 적합

#### 4.4.2 MongoDB (NoSQL)
- **MongoDB 4.4+** 이상 권장  
  - 문서 지향 스키마  
  - 수평 확장(Sharding)에 용이  
  - Django 연동 시에는 ODM(Object Document Mapping) 툴(djongo, mongoengine 등) 사용 가능  
  - 리뷰 내용, 로그 데이터, 이벤트성 데이터 등 **비정형 데이터** 관리에 적합

> **Polyglot Persistence**:  
> - **주요 정형 데이터(예: 사용자, 식당, 리뷰 기본정보)는 MySQL**에,  
> - **비정형 데이터(예: 리뷰 상세 텍스트, 첨부 이미지 메타정보, 로그 등)는 MongoDB**에  
> 병행 사용 가능.

---

## 5. 시스템 아키텍처(System Architecture)

```plaintext
┌────────────┐      ┌────────────────────────┐      ┌───────────┐
│   Client   │  →   │   Next.js (Frontend)   │  →   │   Django   │
│ (Browser)  │      │  - SSR/CSR Rendering   │      │   Backend  │
│            │      │  - TailwindCSS         │      │  - DRF     │
└────────────┘      └────────────────────────┘      └─────┬──────┘
                                                           │
                                                 ┌─────────▼─────────┐
                                                 │    MySQL DB       │
                                                 └─────────┬─────────┘
                                                           │
                                                 ┌─────────▼─────────┐
                                                 │   MongoDB DB       │
                                                 └────────────────────┘
