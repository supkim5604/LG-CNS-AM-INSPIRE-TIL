# [Day 17] LG CNS AM Inspire Camp 7기 TIL

작성일: 2026-11-20  
과목: BE

## 오늘 학습한 주제

- Spring DI Strategy 2 (XML과 어노테이션)
- Spring DI Strategy 3 (어노테이션 기반 설정)

## 오늘 배운 것

어제 배운 **Strategy 1**은 XML에 Bean 등록과 주입 정보를 직접 작성하는 방식이다. 오늘 배운 **Strategy 2**는 XML에서 스캔 범위와 `values.properties`의 위치를 지정하고, Java 코드에서 어노테이션으로 Bean을 등록하고 주입하는 방식이다.

```xml
<context:component-scan base-package="myspring.di.annotation" />
```

| 어노테이션 | 대응하는 XML 설정 | 역할 |
| --- | --- | --- |
| `@Component("stringPrinter")` | `<bean id="stringPrinter" class="..." />` | Bean 등록 |
| `@Autowired` + `@Qualifier("stringPrinter")` | `<property name="printer" ref="stringPrinter" />` | `PrinterBean` 구현체 중 `stringPrinter`를 주입 |
| `@Value("${app.setter.name}")` | `<property name="name" value="어노테이션" />` | 설정값 주입 |

**Strategy 3**은 XML 없이 Java 설정 클래스의 `@Configuration`과 `@ComponentScan` 같은 어노테이션으로 설정하는 방식이다.

## 어려웠던 점 & 해결 과정

아직 Spring DI가 익숙하지 않아서 어떤 객체를 직접 만들고 어떤 객체를 주입받아야 하는지 헷갈린다. 실습에서 `HelloBean`은 `new StringPrinterBean()`을 호출하지 않아도 Spring이 관리하는 `stringPrinter`를 주입받았다.
반면 메서드에서 잠깐 쓸 `ArrayList` 같은 객체는 필요한 곳에서 직접 만들 수 있다. 이번 예제로 컨테이너가 관리하는 의존성과 코드에서 직접 만드는 객체의 차이를 조금 이해했다.

## 내일 계획 & 아직 모르는 것

다음 주부터 Spring Boot를 배운다. 지금까지 이해한 바로는 **Spring Framework**는 Bean 관리와 DI 같은 기반 기능을 제공하고, **Spring Boot**는 그 위에서 자동 설정과 스타터 의존성을 제공해 Spring 애플리케이션을 쉽게 시작할 수 있게 해 준다. 
다음 주에는 지금까지 XML에 적었던 설정 중 어떤 부분을 Boot가 자동으로 처리하는지 확인해 보고 싶다.
