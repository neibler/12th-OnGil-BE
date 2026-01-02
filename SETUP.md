# OnGil Backend - 환경 설정 가이드

## 로컬 개발 환경 설정

### 1. .env 파일 생성

프로젝트 최상위 디렉토리에 `.env` 파일을 생성하세요:

```bash
cp .env.example .env
```

### 2. .env 파일 설정

`.env` 파일을 열어서 다음 값들을 실제 환경에 맞게 수정하세요:

```properties
# 데이터베이스 연결 정보
LOCAL_DB_URL=jdbc:mysql://localhost:3306/ongil?serverTimezone=Asia/Seoul&characterEncoding=UTF-8
LOCAL_DB_USERNAME=root
LOCAL_DB_PASSWORD=your_actual_password
```

#### 필수 환경 변수 설명

- **LOCAL_DB_URL**: MySQL 데이터베이스 연결 URL
  - 형식: `jdbc:mysql://[호스트]:[포트]/[데이터베이스명]?serverTimezone=Asia/Seoul&characterEncoding=UTF-8`
  - 기본값: `jdbc:mysql://localhost:3306/ongil?serverTimezone=Asia/Seoul&characterEncoding=UTF-8`
  
- **LOCAL_DB_USERNAME**: 데이터베이스 사용자 이름
  - 로컬 MySQL 사용자 이름 (예: `root`)
  
- **LOCAL_DB_PASSWORD**: 데이터베이스 비밀번호
  - 로컬 MySQL 비밀번호

### 3. MySQL 데이터베이스 생성

로컬에서 MySQL을 실행하고 다음 명령어로 데이터베이스를 생성하세요:

```sql
CREATE DATABASE ongil CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

### 4. 애플리케이션 실행

```bash
./gradlew bootRun
```

또는

```bash
./gradlew build
java -jar build/libs/12th-OnGil-BE-0.0.1-SNAPSHOT.jar
```

### 5. 프로필 설정

- **local 프로필**: 로컬 개발 환경 (기본값)
  - `.env` 파일의 환경 변수를 사용
  - `application-local.yml` 설정 적용
  
- **prod 프로필**: 프로덕션 환경
  - 환경 변수 `DB_PASSWORD` 사용
  - `application-prod.yml` 설정 적용

프로필을 변경하려면:

```bash
# local 프로필 (기본값)
./gradlew bootRun

# prod 프로필
./gradlew bootRun --args='--spring.profiles.active=prod'
```

또는 환경 변수로 설정:

```bash
export SPRING_PROFILES_ACTIVE=prod
./gradlew bootRun
```

## 주의사항

- `.env` 파일은 **절대 Git에 커밋하지 마세요**. 이 파일에는 민감한 정보(비밀번호 등)가 포함됩니다.
- `.env.example` 파일은 템플릿이므로 Git에 포함됩니다. 실제 값은 포함하지 마세요.
- 새로운 환경 변수가 필요한 경우, `.env.example` 파일에도 추가해 주세요.
