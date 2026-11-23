# LG CNS AM Inspire Camp 7기 TIL

작성일: 2026-11-23  
과목: Spring Framework

## 오늘 학습한 주제

- Spring DI Strategy 3 (어노테이션 기반 설정)

## 오늘 배운 것

지난번에 배운 **Strategy 2**에서는 XML에 Bean을 스캔할 패키지와 `values.properties`의 위치를 적었다. 오늘 배운 **Strategy 3**에서는 이 설정을 `HelloBeanConfig`라는 Java 클래스로 옮겼다.

```java
package myspring.di.annotation.config;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.PropertySource;

@Configuration
@ComponentScan(basePackages = {"myspring.di.annotation"})
@PropertySource(value = "classpath:values.properties")
public class HelloBeanConfig {
}
```

| 어노테이션 | Strategy 2에서 사용한 XML 설정 | 역할 |
| --- | --- | --- |
| `@Configuration` | `<beans>` | Spring이 읽을 Java 설정 클래스임을 표시 |
| `@ComponentScan` | `<context:component-scan>` | `myspring.di.annotation`과 하위 패키지에서 `@Component`가 붙은 클래스를 찾아 Bean으로 등록 |
| `@PropertySource` | `<context:property-placeholder>` | 클래스패스의 `values.properties`를 Spring의 `Environment`에 등록 |

`HelloBean`에서 `@Autowired`와 `@Qualifier("stringPrinter")`로 `stringPrinter`를 주입받는 코드는 Strategy 2에서 배운 방식 그대로 쓸 수 있다. `@Value("${app.setter.name}")`는 `values.properties`에 적힌 `app.setter.name` 값을 주입받는다. [`@Value` 공식 문서](https://docs.spring.io/spring-framework/reference/core/beans/annotation-config/value-annotations.html)

## 어려웠던 점 & 해결 과정

`HelloBeanConfig`의 클래스 본문이 비어 있는데 어떻게 Bean이 등록되는지 헷갈렸다. `@ComponentScan`이 지정된 패키지를 보면서 `@Component`가 붙은 클래스를 찾아 등록한다는 걸 보니 이해가 됐다. `@PropertySource`는 파일을 어디서 읽을지 정하고, `@Value`는 그 파일에서 어떤 키의 값을 가져올지 정한다는 점도 같이 정리했다.

## 내일 계획 & 아직 모르는 것

Spring Boot에서는 `@SpringBootApplication`을 붙인 클래스의 위치에 따라 어디까지 Bean을 스캔하는지 확인해 보고 싶다. `values.properties`의 위치를 직접 지정했던 것처럼 Boot에서 `application.properties`를 읽을 때도 별도 설정이 필요한지 비교해 보고 싶다.
