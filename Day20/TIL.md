# LG CNS AM Inspire Camp 7기 TIL

작성일: 2026-11-25  
과목: Spring Boot  
학습 범위: 교재 13~37쪽, Spring Boot 활용

## 오늘 학습한 주제

- SLF4J 로그 레벨
- Lombok의 `@Builder`로 객체를 생성

## 오늘 배운 것

### MyRunner에서 로그 남기기

`MyRunner`는 Spring Boot가 시작할 때 실행되는 `ApplicationRunner`다. 실습에서는 시작 시 주입된 객체와 설정값을 확인하기 위해 SLF4J의 `Logger`를 사용했다.

```java
Logger logger = LoggerFactory.getLogger(MyRunner.class);

@Override
public void run(ApplicationArguments args) throws Exception {
    System.out.println("Logger 구현 클래스명 = " + logger.getClass().getName());

    logger.debug("CustomVO = {}", customVO);
    logger.debug("myboot.name = {}", myBootName);
    logger.debug("myboot.age = {}", myBootAge);
    logger.debug("myboot.fullName = {}", environment.getProperty("myboot.fullName"));

    logger.info("MyBootProperties getFullName() = {}", properties.getFullName());
    logger.info("MyBootProperties getAge() = {}", properties.getAge());
    logger.info("server.port Program argument 확인 {}", args.containsOption("server.port"));
    logger.info("myboot.name Program argument 확인 {}", args.containsOption("myboot.name"));
}
```

`LoggerFactory.getLogger(MyRunner.class)`는 `MyRunner`의 전체 클래스 이름으로 로거를 가져온다. SLF4J는 코드에서 사용하는 로깅 API이고, 실제 출력은 Logback 같은 구현체가 담당한다. 예제의 `logger.getClass().getName()`으로 실행 중 어떤 구현 클래스가 쓰이는지 확인할 수 있다.

로그 메시지의 `{}`에는 뒤에 전달한 값이 들어간다. `logger.debug("CustomVO = {}", customVO)`처럼 쓰면 DEBUG가 꺼져 있을 때 로그 메시지를 조립하는 일을 피할 수 있다.

기본 로그 레벨인 INFO에서는 예제의 `logger.info()`가 출력된다. `logger.debug()`도 확인하려면 `application.properties`에서 `MyRunner`가 속한 패키지의 레벨을 DEBUG로 설정한다.

```properties
logging.level.com.inspirecamp7.myspringbootproject4.runner=DEBUG
```

### 빌더로 CustomVO 만들기

```java
@Builder
@Getter
@ToString
public class CustomVO {
    private String mode;
    private double rate;
}
```

Lombok의 `@Builder`는 빌더를 만드는 `builder()`, 각 값을 설정하는 `mode()`와 `rate()`, 그리고 실제 객체를 만드는 `build()`를 생성한다. `ProdConfig`에서는 이 메서드들을 이어서 운영 환경의 설정 객체를 만들었다.

```java
@Profile("prod")
@Configuration
public class ProdConfig {
    @Bean
    public CustomVO customVO() {
        return CustomVO.builder()
                .mode("운영 Mode")
                .rate(1.9)
                .build();
    }
}
```

`mode("운영 Mode")`와 `rate(1.9)`를 보면 호출하는 곳에서 각 값의 용도를 바로 알 수 있다. 값을 설정하는 동안에는 빌더에 값이 쌓이고, 마지막에 `build()`를 호출하면 그 값으로 `CustomVO`가 만들어진다.

`prod` 프로파일이 활성화되면 Spring은 이 메서드가 반환한 `CustomVO`를 Bean으로 등록하고, `MyRunner`의 `@Autowired CustomVO customVO`에 주입한다. `@Getter`는 `getMode()`와 `getRate()`를 생성하고, `@ToString`은 객체를 로그에 넣었을 때 필드값을 읽을 수 있게 해 준다. 이 예제에서 DEBUG 로그를 켜면 `CustomVO = CustomVO(mode=운영 Mode, rate=1.9)` 형태로 확인할 수 있다.

## 어려웠던 점 & 해결 과정

`@Builder`는 `CustomVO`를 만드는 코드를 생성하고, `@Bean`은 그렇게 만든 객체를 Spring이 관리하게 한다. 로그에 필드값이 보이는 것은 `@ToString`의 역할이다. 객체를 만드는 곳부터 출력하는 곳까지 따라가 보니 각 어노테이션이 어떤 일을 하는지 구분할 수 있었다.


