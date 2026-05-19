# IoC Container와 Controller

## 1. Spring IoC Container와 빈(Bean) 등록 방식

스프링 컨테이너(IoC Container)는 객체의 생성부터 생명주기 관리, 의존성 주입(DI)을 전담함. 컨테이너가 관리하는 객체를 스프링 빈(Spring Bean)이라고 함.

**1. @Component 기반 자동 등록**

- 클래스 레벨에 선언하여 스프링이 컴포넌트 스캔(Component Scan)을 통해 자동으로 빈을 찾아 컨테이너에 등록하도록 하는 Annotation

- 애플리케이션 구동 시 컨테이너가 객체를 생성하므로 기본 생성자 내부의 로직이 실행됨

```java
@Component
public class ProductController {
    // 스프링 컨테이너에 의해 자동으로 객체가 생성되며 생성자가 호출됨
    public ProductController() {
        System.out.println("ProductController 빈 생성 완료");
    }
}
```

**2. @Configuration + @Bean 기반 수동 등록**

- 개발자가 직접 제어할 수 없는 외부 라이브러리 객체나 설정 정보에 따라 동적으로 빈을 생성해야 할 때 사용
- `@Configuration`이 붙은 설정 클래스 내의 메서드에 `@Bean`을 선언하여 반환되는 객체를 빈으로 등록함.

## 2. Apache Tomcat과 웹 서버 인프라 이해

`Tomcat initialized with port 8080 (http)` 메세지는 스프링 부트 내장 톰캣 서버가 정상적으로 구동되었음을 의미

- Apache Tomcat의 역할: 단순한 웹 서버(Web Server)를 넘어, Java Servlet을 실행하고 동적 페이지를 생성하는 WAS(Web Application Server / Servlet Container) 역할을 수행

- `Port (8080)`: 한 컴퓨터 내에서 실행 중인 수많은 네트워크 프로그램 중 Tomcat 서버를 식별하기 위한 고유 진입 통로(논리적 포트 번호)

- `HTTP Status 404 (Not Found)`: 서버는 정상적으로 켜졌으나, 사용자가 요청한 URL 주소(`http://localhost:8080`)에 매핑된 소스 코드(컨트롤러 메서드)나 정적 자원이 존재하지 않을 때 발생하는 오류

## 3. @Controller와 HTTP 요청 매핑 프로세스

**1. @Controller의 구조와 특징**

- `@Controller` 내부를 보면 `@Component`가 메타 애노테이션으로 포함되어 있어, 별도의 설정 없이도 스프링 빈으로 자동 등록됨
- 웹 MVC 패턴에서 컨트롤러 레이어를 담당, 사용자의 HTTP 요청을 받아 비즈니스 로직으로 중계하는 진입점 역할

**2. 핵심 구성 요소와 매핑 메커니즘**

- `@RequestMapping` 계열 애노테이션: HTTP URL과 특정 메서드를 Mapping

- AnnotatedHandlerMethod 구조: 스프링의 RequestMappingHandlerMapping이 `@Controller` 및 `@RequestMapping`이 적용된 메서드 정보를 스캔하여 메모리에 맵(Map) 형태로 관리

- 핸들러(Handler) 메서드의 동작
  - **일반 메서드**: 소스 코드 내에서 개발자가 직접 호출해야 실행됨
  - **핸들러 메서드**: 사용자가 브라우저 등에서 특정 URL 주소로 HTTP 요청을 보낼 때, 스프링 MVC의 DispatcherServlet에 의해 자동으로 탐색 및 호출됨
