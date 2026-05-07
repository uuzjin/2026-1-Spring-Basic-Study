# Spring MVC 구조와 어노테이션

## Spring MVC의 구조와 역할

### Spring MVC 역할의 분리

> MVC의 핵심: **유지보수의 효율성**을 위해 각 클래스에 명확한 역할을 부여하는 것

- **V(View)**: 사용자에게 보여지는 화면(FE), API 프로젝트에서는 주로 JSON 데이터를 주고받는 형태
- **C(Controller)**: View(사용자)-Model 중간 매개체, Request를 가장 먼저 받으며 요청을 분석해 적절한 Service에 전달하고 결과를 View에 반환
- **M(Model)**: 실제 데이터와 비즈니스 로직이 담김
  - **Service**: 핵심 로직 담당
  - **Repository**: DB와 소통하며 데이터를 저장하거나 불러옴

### 컨트롤러 제작 가이드

- 클래스 이름은 명확하게
- 제어권 위임: 컨트롤러 클래스를 작성하고 나면 스프링 컨테이너가 관리하도록 설정 추가

---

## 어노테이션

```java
class Parent{
    public void method(){
        System.out.println("parent");
    }
}

class Child extends Parent{
    @Override
    public void metod(){
        System.out.println("child");
    }
}
```

위처럼 코드 작성 시 컴파일러가 에러를 띄워줌 (metod)
어노테이션은 실수를 방지하고 의도를 명확히 해줌

#### 어노테이션의 주요 수신자

- **컴파일러**: `@Override`처럼 문법적 오류를 체크하도록 지시
- **빌드도구** (@Getter): 컴파일 시점에 코드를 자동으로 생성
- **프레임워크** (Spring): 스프링에게 관리할 Bean을 알려줌
