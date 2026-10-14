# Mini Dooray
> Spring Boot 기반의 협업 프로젝트 관리 서비스
---
## 🧑‍💻 프로젝트 소개
#### 개발 기간 : 2026.05.14 - 2026.05.22 (9일)
- 본 프로젝트는 프로젝트, 업무(Task), 댓글, 태그, 마일스톤 기능을 제공하는 협업 플랫폼입니다.
- Spring Boot 기반으로 개발되었으며, Spring Security와 Redis Session 기반 인증 구조 및 API 분리 아키텍처를 적용한 **4인 팀 프로젝트**입니다.

### 주요 기능
- 프로젝트 생성 / 수정 / 삭제
- Task CRUD 및 상태 관리
- 댓글 기반 협업 기능
- 태그 및 마일스톤 관리
- 로그인 / 로그아웃 (Spring Security + Redis Session)
- Gateway 기반 API 라우팅

### 핵심 목표 
- 프론트/백엔드 역할 분리 구조 이해
- Gateway 기반 MSA 스타일 API 라우팅 경험
- Redis 기반 Session Clustering을 통한 인증 확장성 확보
- Validation 및 예외 처리 표준화
- API 기반 서비스 통신 구조 설계 경험

### Architecture
```text
Client
   │
   ▼
Front Server
   │
   ▼
Gateway Server 
   │
   ├── Account API
   └── Task API
```

### Service Description
#### Front 
- 사용자 요청 처리
- Thymeleaf 기반 화면 렌더링
- 인증 처리 및 세션 유지
- Gateway API 호출 및 데이터 조합
#### Gateway
- 요청 라우팅
- Account / Task API 분리 연결
#### Account API
- 회원 관리
#### Task API
- 프로젝트 관리
- Task, Comment, Tag, Milestone 기능 제공

---

## 🛠️ Tech Stack
### Develop
<div>
  <img src="https://img.shields.io/badge/java-007396?style=for-the-badge&logo=OpenJDK&logoColor=white">
  <img src="https://img.shields.io/badge/springboot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white">
  <img src="https://img.shields.io/badge/Maven-C71A36?style=for-the-badge&logo=apachemaven&logoColor=white">
  <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=MySQL&logoColor=white">
  <img src="https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white">
  <img src="https://img.shields.io/badge/Thymeleaf-005F0F?style=for-the-badge&logo=Thymeleaf&logoColor=white">
</div>

### Testing & Quality
<div>
  <img src="https://img.shields.io/badge/JUnit5-25A162?style=for-the-badge&logo=junit5&logoColor=white">
  <img src="https://img.shields.io/badge/AssertJ-2E8B57?style=for-the-badge">
  <img src="https://img.shields.io/badge/Mockito-2E8B57?style=for-the-badge">
  <img src="https://img.shields.io/badge/SonarQube-4E9BCD?style=for-the-badge&logo=sonarqube&logoColor=white">
</div>

---

## 🔗 Repository
| Service | Description                           | Repository |
|--|---------------------------------------|---|
| Front | 사용자 UI 및 화면 렌더링 (Thymeleaf 기반), 인증 처리 | [![Repo](https://img.shields.io/badge/GitHub_Repository-Front-181717?style=flat-square&logo=github)](https://github.com/AIoT-3/minidooray-team10-front.git)|
| Gateway | 요청 라우팅                                | [![Repo](https://img.shields.io/badge/GitHub_Repository-Gateway-181717?style=flat-square&logo=github)](https://github.com/AIoT-3/minidooray-team10-gateway.git)|
| Task | 프로젝트 핵심 비즈니스 로직                       | [![Repo](https://img.shields.io/badge/GitHub_Repository-Account-181717?style=flat-square&logo=github)](https://github.com/AIoT-3/minidooray-team10-account-api.git)|
| Account | 회원 핵심 비즈니스 로직                         | [![Repo](https://img.shields.io/badge/GitHub_Repository-Task-181717?style=flat-square&logo=github)](https://github.com/AIoT-3/minidooray-team10-task-api.git)|

---

## 💻 시스템 구조
> 본 프로젝트는 기능별 서비스 분리를 적용하여 개발하였습니다.


### ERD (Entity-Relationship-Diagram)
| account.api | task.api                                              |
|-------------|-------------------------------------------------------|
| <img src="img/account_erd.png" width="200" height="200"> | <img src="img/task_erd.png" width="500" height="400"> |

### 목업
<img width="500" height="450" alt="account_front" src="https://github.com/user-attachments/assets/ebb7ae02-3981-462d-b3f3-8d44df9cdbb8" />
<img width="500" height="450" alt="task_front" src="https://github.com/user-attachments/assets/7dc02f06-19d6-4b61-9b77-e84b5460eb70" />

---

## 🙆🏻‍♀️ 담당 역할
### Task API 구현
...

---

## 🚀 트러블 슈팅 & 설계 개선
### 1. 서비스 간 예외 응답 구조 불일치 문제

#### 문제
- Account API와 Task API가 서로 다른 예외 응답 구조를 사용하여 클라이언트에서 오류 처리를 일관되게 수행하기 어려웠습니다.

#### 원인
- 서비스별 Exception Response 구조 분리
- HTTP Status만으로 비즈니스 예외 구분 어려움
- 프론트에서 예외 처리 로직 증가

#### 해결
- ErrorCode Enum 정의
- 공통 ErrorResponse 구조 도입
- GlobalExceptionHandler 적용
- 예시

  | HTTP Status | Code | Description |
  |------------|------|-------------|
  | 404 | P003 | Project Not Found |
  | 404 | T005 | Task Not Found |
  | 404 | C001 | Comment Not Found |
  | 409 | P012 | Project Already Exists |
  | 403 | N021 | Unauthorized Access |
  | 500 | S500 | Internal Server Error |

#### 결과
- 서비스 간 예외 응답 규격 통일
- 클라이언트의 오류 처리 로직 단순화
- 비즈니스 예외 명확한 구분 가능

### 2. Validation 메시지 우선순위 제어
#### 문제
- 하나의 입력 필드에 여러 Validation 조건이 적용되어 여러 오류 메시지가 동시에 출력되는 UX 문제가 발생했습니다.
#### 원인
- Bean Validation은 모든 제약 조건을 동시에 검증
- 사용자 입장에서 어떤 오류부터 수정해야 하는지 불명확
#### 해결
- @GroupSequence 기반 Validation 순서 정의
- NotBlank → Pattern → Size 순 검증 흐름 구성
- Thymeleaf Validation UI와 연동하여 단일 메시지 출력

#### 결과
- 사용자에게 우선순위 기반 오류 메시지 제공
- UX 개선 (혼란 감소)
- 입력 폼 가독성 향상

---

## 📷 결과물
- Account

| login                                              | signup(validation)                                  | MyPage                                              |
|----------------------------------------------------|-----------------------------------------------------|-----------------------------------------------------|
| <img src="img/login.png" width="400" height="300"> | <img src="img/signup.png" width="400" height="300"> | <img src="img/mypage.png" width="400" height="300"> |

- Task

| Main (Project List)                                    | Project Create                                           | Project Modify                                              |
|--------------------------------------------------------|----------------------------------------------------------|-------------------------------------------------------------|
| <img src="img/main.png" width="400" height="300">      | Main에서 이름으로 생성                                           | <img src="img/project_modify.png" width="350" height="350"> |
| Task List                                              | Task Create                                              | Task Detail                                                 |
| <img src="img/task_list.png" width="400" height="300"> | <img src="img/task_create.png" width="400" height="400"> | <img src="img/task_detail.png" width="400" height="400">    |

---

## 🌱 회고 및 개선 예정 사항
### 💬 회고
- 단기 프로젝트 특성상 기능 구현에 집중하면서 Validation을 단순하게 처리했으나, 사용자 경험 측면에서 입력 검증의 중요성을 체감했습니다.
- Spring MVC + Thymeleaf 기반 SSR 구조에서 Validation 실패 시 화면 재구성 로직이 Controller에 집중되는 구조적 한계를 경험했습니다.
- Front / Gateway / API 분리 구조를 통해 계층별 책임 분리의 중요성을 이해했습니다.
- Redis Session Clustering을 통해 분산 환경에서 인증 상태를 유지하는 구조를 설계하는 경험을 했습니다.

### 리팩토링 예정
- Spring Cloud Netflix Eureka 기반 Service Discovery 적용
- Front Server 책임 분리 (Service Layer 강화)
- Validation 일부를 JavaScript 기반 사전 검증으로 이동
- Controller의 View Model 생성 로직 Service Layer로 이동
- SonarQube 기반 코드 품질 개선
