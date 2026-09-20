# AjouFinder

**교내 분실물과 발견물을 한곳에서 관리하는 백엔드**

`Java 17` · `Spring Boot 3.3.5` · `JPA / QueryDSL` · `MySQL` · `Redis` · `JWT`

개인 프로젝트로 진행한 분실물·발견물 관리 서비스입니다. 게시물과 위치, 처리 상태를 연결해 물건을 찾는 과정을 지원합니다.

## 주요 기능

| 기능 | 내용 | 코드 |
| --- | --- | --- |
| 게시물 | 분실·발견 게시글 CRUD, 날짜·위치 등 필터, 처리·해결 상태 | [BoardController](ajoufinder/src/main/java/com/ajoufinder/api/controller/board/BoardController.java) |
| 위치 | 위치 등록·조회·수정·활성화 | [LocationController](ajoufinder/src/main/java/com/ajoufinder/api/controller/location/LocationController.java) |
| 회원 | 가입·로그인, 사용자 게시물 조회 | [UserController](ajoufinder/src/main/java/com/ajoufinder/api/controller/user/UserController.java) |
| 인증 | 이메일 검증, 닉네임 중복 확인 | [AuthController](ajoufinder/src/main/java/com/ajoufinder/api/controller/auth/AuthController.java) |

## 설계 살펴보기

- `api`: 컨트롤러와 서비스. 게시물·회원에서 조회와 변경 서비스를 분리합니다.
- `domain`: 엔티티와 저장소. [게시판 QueryDSL 조회](ajoufinder/src/main/java/com/ajoufinder/domain/board/repository/custom/BoardRepositoryCustomImpl.java)를 확인할 수 있습니다.
- `common`: 보안·공통 설정과 예외 처리.

## 실행 조건

프로젝트 루트가 아닌 **`ajoufinder/` 하위 폴더**에 Gradle 애플리케이션이 있습니다.

```bash
git clone https://github.com/InaJeong73/AjouFinder.git
cd AjouFinder/ajoufinder
./gradlew bootRun
```

Windows는 `.\gradlew.bat bootRun`을 사용합니다. JDK 17과 별도 DB·메일·인증 환경 설정이 필요합니다. 현재 저장소에는 실행용 `application.yml`이 포함되지 않아 위 명령만으로 바로 기동되지는 않습니다. 운영 자격증명 대신 개인 개발용 설정을 준비해야 합니다.

## API 빠른 안내

| 경로 | 역할 |
| --- | --- |
| `/register`, `/login` | 회원가입·로그인 |
| `/api/v1/boards/lost`, `/api/v1/boards/found` | 게시글 등록·목록 |
| `/api/v1/boards/{boardId}` | 상세조회·수정·삭제 |
| `/api/v1/locations` | 위치 관리 |
| `/api/v1/auth/email/verify` | 이메일 검증 |

상세 요청·응답은 링크한 컨트롤러와 DTO를 기준으로 확인합니다.

<details>
<summary>프로젝트 화면</summary>

![AjouFinder 화면 1](https://github.com/user-attachments/assets/358c29e8-cae5-47c2-a9a6-4ff033566c8e)
![AjouFinder 화면 2](https://github.com/user-attachments/assets/4b3af381-5d98-426d-8a53-044159a86889)

</details>

## 다음 개선 후보

로컬 설정 예제와 재현 가능한 테스트 데이터, 필터 조합·페이지 경계 테스트를 보강할 예정입니다. 아직 완료한 기능이나 성능 성과로 표시하지 않습니다.
