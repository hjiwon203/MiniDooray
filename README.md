# Mini Dooray
> Spring Boot 기반의 협업 프로젝트 관리 서비스 (4인 팀 · MSA 구조)

---

## 🧑‍💻 프로젝트 소개
#### 개발 기간 : 2026.05.14 - 2026.05.22 (9일)
- 프로젝트, 업무(Task), 댓글, 태그, 마일스톤 기능을 제공하는 협업 플랫폼입니다.
- Front / Gateway / Account API / Task API 4개 서버로 나눈 **4인 팀 프로젝트**이며, 저는 **Task API를 팀원 1명과 함께 담당**했습니다.

### Architecture
```text
Client
   │
   ▼
Front Server (Thymeleaf, Redis Session)
   │
   ▼
Gateway Server
   │
   ├── Account API   (회원)
   └── Task API      (프로젝트 · 업무 · 댓글 · 태그 · 마일스톤)  ◀ 담당
```

### 주요 기능
- 프로젝트 생성 / 수정 / 삭제, 멤버 초대
- 업무(Task) CRUD 및 상태 관리 (TODO · IN_PROGRESS · DONE)
- 댓글 기반 협업
- 태그 및 마일스톤 관리
- 로그인 / 로그아웃 (Spring Security + Redis Session)
- Gateway 기반 API 라우팅

### Service Description
| 서버 | 역할 |
|--|--|
| Front | 사용자 요청 처리, Thymeleaf 화면 렌더링, 인증 및 Redis 세션 유지, Gateway API 호출 및 데이터 조합 |
| Gateway | 요청 라우팅, Account / Task API 분리 연결 |
| Account API | 회원 가입 · 정보 · 상태 관리 |
| **Task API** | 프로젝트 · 멤버 · 업무 · 댓글 · 태그 · 마일스톤 관리 **(담당)** |

Gateway에서 인증을 마친 요청은 `X-USER-ID` 헤더로 사용자 식별자를 실어 Task API로 전달되고, Task API는 이 값으로 프로젝트 멤버 여부와 작성자 본인 여부를 검증합니다.

---

## 🛠️ Tech Stack

| 분류 | 프로젝트 전체 | Task API (담당) |
|--|--|--|
| **Language** | <img src="https://img.shields.io/badge/Java_21-007396?style=flat-square&logo=openjdk&logoColor=white"> | <img src="https://img.shields.io/badge/Java_21-007396?style=flat-square&logo=openjdk&logoColor=white"> |
| **Framework** | <img src="https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white"> <img src="https://img.shields.io/badge/Spring_Data_JPA-6DB33F?style=flat-square&logo=spring&logoColor=white"> <img src="https://img.shields.io/badge/Spring_Security-6DB33F?style=flat-square&logo=springsecurity&logoColor=white"> <img src="https://img.shields.io/badge/Thymeleaf-005F0F?style=flat-square&logo=thymeleaf&logoColor=white"> | <img src="https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white"> <img src="https://img.shields.io/badge/Spring_Data_JPA-6DB33F?style=flat-square&logo=spring&logoColor=white"> |
| **Database / Cache** | <img src="https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white"> <img src="https://img.shields.io/badge/H2-09476B?style=flat-square"> <img src="https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white"> | <img src="https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white"> <img src="https://img.shields.io/badge/H2-09476B?style=flat-square"> |
| **Test** | <img src="https://img.shields.io/badge/JUnit_5-25A162?style=flat-square&logo=junit5&logoColor=white"> <img src="https://img.shields.io/badge/Mockito-78A641?style=flat-square"> | <img src="https://img.shields.io/badge/JUnit_5-25A162?style=flat-square&logo=junit5&logoColor=white"> <img src="https://img.shields.io/badge/Mockito-78A641?style=flat-square"> |
| **Build** | <img src="https://img.shields.io/badge/Maven-C71A36?style=flat-square&logo=apachemaven&logoColor=white"> | <img src="https://img.shields.io/badge/Maven-C71A36?style=flat-square&logo=apachemaven&logoColor=white"> |

---

## 🔗 Repository
| Service | Description | Repository |
|--|--|--|
| Front | 사용자 UI 및 화면 렌더링 (Thymeleaf), 인증·세션 | [![Repo](https://img.shields.io/badge/GitHub_Repository-Front-181717?style=flat-square&logo=github)](https://github.com/AIoT-3/minidooray-team10-front) |
| Gateway | 요청 라우팅 | [![Repo](https://img.shields.io/badge/GitHub_Repository-Gateway-181717?style=flat-square&logo=github)](https://github.com/AIoT-3/minidooray-team10-gateway) |
| Account API | 회원 비즈니스 로직 | [![Repo](https://img.shields.io/badge/GitHub_Repository-Account-181717?style=flat-square&logo=github)](https://github.com/AIoT-3/minidooray-team10-account-api) |
| **Task API** | 프로젝트 핵심 비즈니스 로직 **(담당)** | [![Repo](https://img.shields.io/badge/GitHub_Repository-Task-181717?style=flat-square&logo=github)](https://github.com/AIoT-3/minidooray-team10-task-api) |

---

## 💻 시스템 구조
> 기능별로 서비스를 분리해 개발했습니다.

### ERD
<table>
  <tr>
    <td align="center" valign="top"><b>account-api</b><br/><img src="https://raw.githubusercontent.com/hjiwon203/MiniDooray/main/img/account_erd.png" width="270"></td>
    <td align="center" valign="top"><b>task-api</b><br/><img src="https://raw.githubusercontent.com/hjiwon203/MiniDooray/main/img/task_erd.png" width="520"></td>
  </tr>
</table>

### 목업
<img width="400" alt="account_front" src="https://github.com/user-attachments/assets/ebb7ae02-3981-462d-b3f3-8d44df9cdbb8" />
<img width="400" alt="task_front" src="https://github.com/user-attachments/assets/7dc02f06-19d6-4b61-9b77-e84b5460eb70" />

### Task API 도메인 구조

```
Project ─┬─ ProjectMember (ADMIN / MEMBER)
         ├─ Milestone
         ├─ Tag
         └─ Task ─┬─ Comment
                  └─ TaskTag ── Tag   (N:M 해소용 중간 엔티티)
```

---

## 🙆🏻‍♀️ 담당 역할

Task API를 2인이 나눠 맡았고, 저는 **업무(Task) · 댓글(Comment) · 태그(Tag)** 도메인과 **공통 예외 처리**를 구현했습니다.
(프로젝트 · 멤버 · 마일스톤 · 권한 검증 AOP · 회원 탈퇴 연쇄 정리는 팀원 담당)

| 영역 | 구현 내용 |
|--|--|
| 업무(Task) | 업무 목록·상세 조회, 생성, 수정, 삭제 API / 업무-태그 N:M 매핑 / 마일스톤 연결 |
| 댓글(Comment) | 댓글 등록·수정·삭제 API, 작성자 본인만 수정·삭제하도록 검증 |
| 태그(Tag) | 프로젝트 단위 태그 관리 서비스, 프로젝트 소속 태그 일괄 조회 쿼리 |
| 프로젝트 목록 | 사용자별 프로젝트 목록을 **상태별 필터 + 최신순 페이징**으로 조회, 공통 `PageResponse` |
| 예외 처리 | `ErrorCode` · `BaseException` · `GlobalExceptionHandler`로 에러 응답 형식 통일 |
| 테스트 | Task·Tag·Milestone 서비스, Task·Comment·Milestone 리포지토리, Project·Tag 컨트롤러 테스트 |

---

## 🚀 트러블 슈팅 & 설계 개선

### 1. 업무 목록 조회 시 N+1 문제
#### 문제
- 업무 목록을 조회하면 업무마다 마일스톤과 태그를 가져오는 쿼리가 추가로 나가, 업무 수만큼 쿼리가 늘어났습니다. 상세 조회에서는 태그가 비어서 나오는 문제도 있었습니다.
#### 원인
- `Task → Milestone`, `Task → TaskTag → Tag` 연관관계가 지연 로딩이라, 응답 DTO로 변환하는 시점에 연관 엔티티마다 쿼리가 실행됨
#### 해결
- 목록·상세 조회를 **fetch join** 쿼리로 바꿔 업무, 마일스톤, 태그를 한 번에 조회
- 컬렉션 fetch join으로 생기는 중복 행은 `distinct`로 제거
```java
select distinct t
from Task t
join fetch t.milestone
left join fetch t.taskTags tt
left join fetch tt.tag
where t.project.id = :projectId
```
#### 결과
- 업무 수와 관계없이 조회 쿼리 1회로 목록 응답 구성, 상세 조회의 태그 누락 해결

### 2. 업무 수정 시 태그 변경 처리와 프로젝트 경계 검증
#### 문제
- 업무 수정 요청에는 최종 태그 목록이 통째로 오는데, 기존 매핑을 모두 지우고 다시 넣으면 불필요한 삭제·삽입이 생깁니다.
- 또 태그 ID만 받기 때문에 **다른 프로젝트의 태그 ID**를 넣어도 업무에 연결될 수 있었습니다.
#### 해결
- 현재 태그와 요청 태그를 비교해 **빠진 태그만 제거하고 새 태그만 추가**하도록 구현 (`orphanRemoval`로 중간 엔티티 정리)
- 태그 조회를 `where project.id = :projectId and id in :tagIds` 한 번으로 처리하고, 조회 건수가 요청 건수와 다르면 `INVALID_TAG`로 거절
- 업무 생성 시 마일스톤도 해당 프로젝트 소속인지 확인
#### 결과
- 태그 변경 시 바뀐 매핑만 반영, 프로젝트 간 데이터 섞임 차단

### 3. 예외 응답 형식 통일
#### 문제
- 예외마다 응답 형태가 달라 Front에서 오류를 일관되게 처리하기 어려웠습니다.
#### 해결
- `ErrorCode` Enum(HTTP 상태 + 서비스 코드 + 메시지)과 공통 `ErrorResponse` 정의
- `GlobalExceptionHandler`에서 비즈니스 예외, `@Valid`/`@Validated` 검증 실패, 예상하지 못한 예외를 각각 처리

  | HTTP Status | Code | Description |
  |--|--|--|
  | 404 | K005 | 업무를 찾을 수 없음 |
  | 404 | C001 | 댓글을 찾을 수 없음 |
  | 400 | T032 | 유효하지 않은 태그 |
  | 400 | R031 | 입력값 검증 실패 |
  | 403 | N021 | 접근 권한 없음 |
  | 500 | S500 | 서버 내부 오류 |
#### 결과
- 서비스 간 예외 응답 규격 통일
- 클라이언트의 오류 처리 로직 단순화
- 비즈니스 예외 명확한 구분 가능

---

## 📷 결과물

### Account
<table>
  <tr>
    <td align="center" valign="top"><b>로그인</b><br/><img src="https://raw.githubusercontent.com/hjiwon203/MiniDooray/main/img/login.png" width="260"></td>
    <td align="center" valign="top"><b>회원가입 (검증)</b><br/><img src="https://raw.githubusercontent.com/hjiwon203/MiniDooray/main/img/signup.png" width="260"></td>
    <td align="center" valign="top"><b>마이페이지</b><br/><img src="https://raw.githubusercontent.com/hjiwon203/MiniDooray/main/img/mypage.png" width="260"></td>
  </tr>
</table>

### Project
<table>
  <tr>
    <td align="center" valign="top"><b>메인 · 프로젝트 목록</b><br/><img src="https://raw.githubusercontent.com/hjiwon203/MiniDooray/main/img/main.png" width="400"></td>
    <td align="center" valign="top"><b>프로젝트 수정</b><br/><img src="https://raw.githubusercontent.com/hjiwon203/MiniDooray/main/img/project_modify.png" width="400"></td>
  </tr>
</table>

> 프로젝트 생성은 메인 화면에서 이름을 입력해 바로 만듭니다.

### Task
<table>
  <tr>
    <td align="center" valign="top"><b>업무 목록</b><br/><img src="https://raw.githubusercontent.com/hjiwon203/MiniDooray/main/img/task_list.png" width="260"></td>
    <td align="center" valign="top"><b>업무 생성</b><br/><img src="https://raw.githubusercontent.com/hjiwon203/MiniDooray/main/img/task_create.png" width="260"></td>
    <td align="center" valign="top"><b>업무 상세</b><br/><img src="https://raw.githubusercontent.com/hjiwon203/MiniDooray/main/img/task_detail.png" width="260"></td>
  </tr>
</table>

---

## 🌱 회고 및 개선 예정 사항
### 💬 회고
- 서비스를 나눈 구조에서는 회원 엔티티를 직접 참조할 수 없어, Gateway가 넘겨주는 사용자 ID만으로 권한과 데이터 경계를 지켜야 한다는 점을 배웠습니다.
- JPA 지연 로딩이 DTO 변환 시점에 쿼리를 만든다는 것을 직접 겪고, 조회 패턴에 맞춰 fetch join을 설계하는 습관이 생겼습니다.
- 2인이 한 서버를 나눠 개발하면서 예외 코드와 응답 형식을 먼저 맞춰 두는 것이 협업 비용을 크게 줄인다는 것을 느꼈습니다.

### 개선 예정
- 업무 **수정** 시에도 마일스톤의 프로젝트 소속 검증 추가 (현재는 생성 시에만 확인)
- 업무 목록에 페이징 적용 (컬렉션 fetch join과 페이징을 함께 쓰기 위해 `@BatchSize` 등 검토)
- 주석으로 남은 이전 구현 코드 정리
