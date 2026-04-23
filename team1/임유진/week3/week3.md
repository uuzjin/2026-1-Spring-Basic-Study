## API

### 웹 개발 패러다임의 변화

- 과거: 화면과 로직이 뒤섞여 유지보수가 힘든 형태
- 현재: 프론트엔드(화면)와 백엔드(데이터/로직)의 명확한 분리
- 이유: 사용자 상호작용의 증가로 인해 데이터 처리 로직이 고도화되었고, 각 영역의 전문성을 높여 개발 효율을 극대화하기 위함

### API와 Interface

백엔드 개발자의 주 업무는 API 제작

- Interface (인터페이스): 서로 다른 두 시스템이 상호작용할 수 있게 도와주는 접점
- API (Application Programming Interface): 프론트엔드나 외부 시스템이 백엔드의 기능이나 데이터에 접근할 수 있도록 열어둔 통로
- 사용 이유: 내부 시스템의 복잡한 구조를 숨기고(캡슐화), 정해진 규칙으로만 데이터에 접근하게 하여 보안과 안정성을 지키기 위함

#### API 더 알아보기

- REST API: HTTP라는 통신 규약을 최대한 활용하여 설계된 API 스타일
- RESTful API: REST 설계 원칙을 매우 충실하게 잘 지킨 API
- HTTPS: HTTP에 Secure을 더한 것, 데이터를 암호화하여 주고받기 때문에 보안이 훨씬 강력함

---

## Spring Boot 프로젝트 시작하기

### 주요 용어 정리

- 빌드 (Build): 작성한 소스코드를 컴퓨터가 실행할 수 있는 형태(`.jar`, `.war`)로 변환하는 전체 과정
- 빌드 도구 (Build Tool): 이 빌드 과정을 자동화해 주는 도구 (Gradle, Maven 등)
- 배포 (Deployment): 빌드된 결과물을 실제 서버에 올려서 사용자들이 접속할 수 있게 만드는 것
- 의존성 (Dependencies): 다른 라이브러리나 프레임워크 기능을 '사용'하는 관계

### 프로젝트 세팅

- https://start.spring.io/
- Project: Gradle - Groovy (최근 가장 선호되는 빌드 도구)
- Language: Java
- Spring Boot: v.3.5.13 (안정적인 최신 버전 선택)
- Packaging: JAR (Java Archive). 내장 웹 서버(Tomcat)를 포함하고 있어서 어디서든 단일 파일로 실행 가능해 편리해. (전통적인 WAR 방식보다 권장됨)
- Java Version: 17
- Dependencies: Spring Web (웹 API 개발을 위한 핵심 라이브러리)

### 폴더 구조 알아보기

<div style="display: flex; justify-content: center; gap: 10px;">
  <img src="https://velog.velcdn.com/images/lyj5721/post/ad279cb2-c6c8-4370-98c4-f2063abcfec0/image.png" style="width: 45%;">
  <img src="https://velog.velcdn.com/images/lyj5721/post/70b8d7c7-e997-411a-add5-0106b71810c8/image.png" style="width: 45%;">
</div>

| 폴더                | 파일                                                                   |
| ------------------- | ---------------------------------------------------------------------- |
| .gradle             | Gradle 필드 도구가 사용하는 캐시 파일이 들어 있음                      |
| build               | 빌드를 수행한 결과물이 저장                                            |
| src/main            | 실제 소스 코드와 설정 파일(resources)이 위치하는 메인 공간             |
| src/test            | 코드의 안정성을 검증하기 위한 테스트 코드를 작성하는 곳                |
| build.gradle        | 프로젝트의 설정 정보와 의존성을 관리하는 문서                          |
| gradlew/gradlew.bat | Gradle 설치 없이도 빌드를 실행할 수 있게 해주는 래퍼(Wrapper) 스크립트 |

### 실행

```java
@SpringBootApplication
public class DemoApplication {

	public static void main(String[] args) {
		SpringApplication.run(DemoApplication.class, args);
	}

}

```

![](https://velog.velcdn.com/images/lyj5721/post/349000ae-17b0-4ac0-82b6-03e23013aed7/image.png)

위 main 함수 실행 -> `Started DemoApplication` 로그와 함께 정상 실행 확인
