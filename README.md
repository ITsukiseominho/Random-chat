# Random-chat
한국교통대학교 자바프로그래밍 과제 랜덤 채팅앱 
# 💬 실시간 채팅 애플리케이션

Spring Boot + WebSocket + MySQL을 사용한 실시간 채팅 애플리케이션입니다.

## 🚀 기능

- ✅ 회원가입/로그인 (Spring Security)
- ✅ 실시간 채팅 (WebSocket + STOMP)
- ✅ 채팅방 생성/참여/나가기
- ✅ 참여자 관리 및 입장알림
- ✅ 메시지 영구 저장 (MySQL)
- ✅ 사용자 프로필 색상 자동 할당
- ✅ 무지개 반응형 UI

## 📋 기술 스택

- **Backend**: Spring Boot 3.2.0, Spring Security, Spring Data JPA
- **Frontend**: Thymeleaf, HTML5, CSS3, JavaScript
- **WebSocket**: STOMP, SockJS
- **Database**: MySQL 8.0
- **Build Tool**: Maven
- **Java**: 17

## 📁 프로젝트 구조

```
chatapp_extracted/
├── pom.xml
├── .idea/
│   ├── compiler.xml
│   ├── misc.xml
│   ├── workspace.xml
│   └── dataSources/
│       └── ... (IntelliJ 설정파일들)
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com.example.chatapp/
│   │   │       ├── ChatAppApplication.java
│   │   │       ├── config/
│   │   │       │   └── WebSocketConfig.java
│   │   │       ├── controller/
│   │   │       │   ├── ChatController.java
│   │   │       │   ├── RandomChatController.java
│   │   │       │   └── UserController.java
│   │   │       ├── dto/
│   │   │       │   ├── ChatMessage.java
│   │   │       │   ├── RandomChatMessage.java
│   │   │       │   └── UserDto.java
│   │   │       ├── handler/
│   │   │       │   ├── ChatWebSocketHandler.java
│   │   │       │   └── RandomChatWebSocketHandler.java
│   │   │       ├── model/
│   │   │       │   └── User.java
│   │   │       ├── repository/
│   │   │       │   └── UserRepository.java
│   │   │       └── service/
│   │   │           ├── ChatService.java
│   │   │           ├── RandomChatService.java
│   │   │           └── UserService.java
│   │   ├── resources/
│   │   │   ├── application.yml
│   │   │   ├── static/
│   │   │   │   └── images/
│   │   │   │       └── knut.png
│   │   │   └── templates/
│   │   │       ├── chat.html
│   │   │       ├── login.html
│   │   │       ├── random.html
│   │   │       └── register.html
│   └── generated-sources/
│       └── annotations/
└── target/
    └── ... (빌드된 클래스 파일들)

```

## 🔧 설치 및 실행

### 1. MySQL 데이터베이스 생성

```sql
CREATE DATABASE chatapp CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

### 2. 프로젝트 클론 또는 생성

IntelliJ IDEA에서 New Project → Spring Initializr 선택:
- Name: `chatapp`
- Type: **Maven**
- Java: **17**
- Dependencies: Web, JPA, MySQL, Security, Thymeleaf, WebSocket, Lombok

### 3. 설정 파일 수정

`src/main/resources/application.properties` 파일에서 MySQL 비밀번호 수정:

```properties
spring.datasource.password=your_password  # 실제 비밀번호로 변경
```

### 4. 프로젝트 실행

```bash
mvn spring-boot:run
```

또는 IntelliJ에서 `ChatappApplication.java` 실행

### 5. 접속

브라우저에서 `http://localhost:8080` 접속

사용 끝
---

✅ 2번. 폴더별 역할 설명 
📁 src/main/java/com.example.chatapp/

최상위 Java 패키지. 백엔드 핵심 코드들이 여기에 들어있음.

📁 config/

WebSocketConfig.java
WebSocket endpoint(채팅 주소) 등록하는 곳.
예: /ws/chat, /ws/random 같은 URL을 웹소켓으로 사용하도록 함.

📁 controller/

사용자 요청(HTTP 요청) 받고 처리하는 클래스들.

ChatController → 일반 채팅 페이지 이동 담당

RandomChatController → 랜덤채팅 페이지 이동 담당

UserController → 로그인/회원가입 처리

📁 dto/

데이터 전송 객체(프론트 ↔ 서버에서 주고받는 메시지 형태)

ChatMessage → 기본 채팅 메시지 구조

RandomChatMessage → 랜덤 채팅 메시지 구조

UserDto → 회원가입/로그인에 사용

📁 handler/

WebSocket 실시간 통신을 처리하는 핵심 파일들.

ChatWebSocketHandler
일반 1:N 채팅 기능 처리 (메시지 브로드캐스트)

RandomChatWebSocketHandler
랜덤 매칭된 두 사람끼리 채팅 처리

📁 model/

User.java → DB에 저장되는 User 엔티티

📁 repository/

UserRepository → JPA로 DB의 user 테이블에 접근하는 역할

📁 service/

실제 로직 담당

ChatService → 채팅 관련 기능

RandomChatService → 랜덤 매칭 로직

UserService → 회원가입/로그인 로직

📁 resources/application.yml

DB 접속 정보, 포트 번호, WebSocket 설정 같은 환경 설정 파일.

📁 resources/templates/

HTML 템플릿 파일들

login.html

register.html

chat.html

random.html

스프링 부트 + Thymeleaf로 렌더링됨.

📁 resources/static/

정적 리소스(css, js, 이미지)
현재는 knut.png 만 있음.

✅ 4번. ZIP 내부 코드 분석 (핵심만 정확하게)

업로드한 ZIP은 Spring Boot + WebSocket 기반 채팅 앱임.

✔ 기능 구조

일반 채팅방 (1개의 방에 전체 참여)

랜덤 채팅 (1:1 매칭 후 WebSocket 열림)

회원 가입/로그인 기능

템플릿(Thymeleaf) 기반 프론트엔드

MySQL 연동

WebSocket 핸들러로 실시간 메시지 송수신

✔ 코드 수준 분석

WebSocketConfig에서 endpoint를 SockJS 없이 기본 WebSocket으로 지정

Handler들은 TextWebSocketHandler 확장

메시지를 JSON 파싱 후 broadcasting

RandomChatService는 간단한 큐 방식으로 매칭 진행

UserService는 암호화 없이 비밀번호 저장 → 보안 약함

HTML에서 WebSocket 연결은 JS로 직접 구현 → 간단하지만 실시간 기능 충분

전체적으로 학습용/테스트용 수준의 WebSocket 채팅 프로젝트

✔ 문제점

비밀번호 암호화 없음

예외 처리 매우 부족

WebSocket 인증 없음(로그인 검증 X)

배포 환경 설정 없음

✅ 5번. 프로젝트 실행 방법 
1) MySQL 데이터베이스 만들기
CREATE DATABASE websocket_chat CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

2) application.yml 수정
spring:
  datasource:
    username: (너의 MySQL 계정)
    password: (너의 비밀번호)

3) Maven 빌드

IntelliJ에서:

mvn clean install


또는 터미널에서:

./mvnw clean package

4) 서버 실행

IntelliJ: ChatAppApplication 실행
터미널:

java -jar target/chatapp-0.0.1-SNAPSHOT.jar

5) 웹에서 접속

브라우저 입력:

로그인:

http://localhost:8080/login


일반 채팅:

http://localhost:8080/chat


랜덤 채팅:

http://localhost:8080/random
