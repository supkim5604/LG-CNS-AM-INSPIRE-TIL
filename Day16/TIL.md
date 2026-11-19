# [Day 16] LG CNS AM Inspire Camp 7기 TIL

작성일: 2026-11-19

과목: BE

## 오늘 학습한 주제
- Spring Framework와 IoC
- Spring Bean, BeanFactory, ApplicationContext
- Configuration Metadata
- DI (Dependency Injection)
  - Setter Injection
  - Constructor Injection
- Bean Scope (Singleton, Prototype)

## 오늘 배운 것

### Spring Framework와 IoC

Spring Framework는 Java 기반 애플리케이션 개발을 지원하는 프레임워크이다.

Spring의 핵심 개념 중 하나인 **IoC(Inversion of Control)**는 제어의 역전을 의미한다.

기존 Java에서는 개발자가 `new` 키워드를 이용하여 객체를 직접 생성하고 관리하였다. 하지만 Spring에서는 객체의 생성과 관리에 대한 제어권을 **Spring IoC Container**에 맡길 수 있다.

Spring IoC Container와 관련된 용어는 다음과 같다.

- **Bean**: Spring Container가 생성하고 관리하는 객체
- **BeanFactory**: Bean 생성, 관리 및 의존성 주입 기능을 제공하는 기본 IoC Container 인터페이스
- **ApplicationContext**: BeanFactory의 기능을 확장한 인터페이스로, Bean 관리 외에도 다양한 부가 기능을 제공한다.
- **Configuration Metadata**: Spring Container가 Bean을 생성하고 의존성을 설정하는 데 사용하는 설정 정보이다. XML, Annotation, Java Configuration 방식 등이 있다.

###  DI (Dependency Injection)

DI는 의존성 주입이라는 의미로, 객체가 필요로 하는 다른 객체를 직접 생성하지 않고 외부에서 전달받는 방식이다.

Spring에서는 XML 설정 파일을 통해 의존성을 주입할 수 있다.

오늘은 Setter Injection과 Constructor Injection 두 가지 방식을 배웠다.

###  Setter Injection

Setter 메서드를 이용하여 객체의 의존성을 주입하는 방식이다.

```xml
<!-- StringPrinter Bean 등록 -->
<bean id="strPrinter"
      class="myspring.di.xml.StringPrinter" />

<!-- Hello Bean 등록 -->
<bean id="hello"
      class="myspring.di.xml.Hello"
      scope="singleton">

    <property name="name" value="스프링" />
    <property name="printer" ref="strPrinter" />

</bean>
```

`<property>` 태그를 사용하여 Setter 메서드를 호출하는 방식으로 값을 주입한다.

- `name`: 주입할 프로퍼티 이름
- `value`: 문자열, 숫자 등 일반적인 값 주입
- `ref`: 다른 Spring Bean을 참조하여 주입

위 XML 설정은 다음과 같은 Java 코드와 유사하다.

```java
Hello hello = new Hello();
hello.setName("스프링");
hello.setPrinter(new StringPrinter());
```

단, 실제 Spring에서는 `StringPrinter` 객체를 Container가 관리하고 `hello` Bean에 주입한다.

###  Constructor Injection

생성자를 통해 객체 생성 시점에 의존성을 주입하는 방식이다.

```xml
<!-- ConsolePrinter Bean 등록 -->
<bean id="conPrinter"
      class="myspring.di.xml.ConsolePrinter" />

<!-- Hello Bean 등록 -->
<bean id="hellocCons"
      class="myspring.di.xml.Hello">

    <constructor-arg index="0" value="생성자" />
    <constructor-arg index="1" ref="conPrinter" />

</bean>
```

`<constructor-arg>` 태그를 이용하여 생성자의 매개변수에 값을 전달한다.

- `index`: 생성자 매개변수의 순서 (0부터 시작)
- `value`: 일반적인 값 전달
- `ref`: 다른 Spring Bean 객체 전달

위 설정은 다음 Java 코드와 유사하다.

```java
Hello hello =
    new Hello("생성자", new ConsolePrinter());
```

Setter Injection은 객체 생성 후 Setter 메서드로 의존성을 주입하지만, Constructor Injection은 객체 생성 시점에 의존성을 주입한다는 차이가 있다.

###  Bean Scope

Bean Scope는 Spring Container가 Bean 인스턴스를 생성하고 관리하는 범위를 의미한다.

오늘은 Singleton과 Prototype을 배웠다.

**Singleton**

```xml
<bean id="hello"
      class="myspring.di.xml.Hello"
      scope="singleton" />
```

- Spring Container 내에서 해당 Bean 정의에 대해 하나의 인스턴스를 관리한다.
- 여러 번 조회해도 동일한 객체를 반환한다.
- Spring Bean의 기본 Scope이다.

**Prototype**

```xml
<bean id="hello"
      class="myspring.di.xml.Hello"
      scope="prototype" />
```

- Bean을 요청할 때마다 새로운 객체를 생성한다.
- 조회할 때마다 서로 다른 객체가 반환된다.
- Spring은 Prototype Bean을 생성하고 초기화한 후, 일반적으로 이후의 생명주기를 관리하지 않는다.

예를 들어 동일한 Bean을 두 번 조회한다면 다음과 같은 차이가 있다.

```java
Hello hello1 = context.getBean("hello", Hello.class);
Hello hello2 = context.getBean("hello", Hello.class);

System.out.println(hello1 == hello2);
```

- `singleton` → `true`
- `prototype` → `false`

## 오늘 배운 내용 정리

오늘은 Spring Framework의 IoC와 DI 개념을 배우고 XML 설정 파일을 통해 Bean을 등록하고 의존성을 주입하는 방법을 학습하였다.
`<property>`와 `<constructor-arg>` 태그를 사용하여 Setter Injection과 Constructor Injection의 차이를 확인하였다. 또한 Bean Scope에 따라 Singleton은 같은 객체를 반환하고 Prototype은 새로운 객체를 생성한다는 점을 알게 되었다.


- **IoC**: 객체 생성과 관리의 제어권을 Spring Container에 맡기는 것
- **DI**: 객체가 필요로 하는 의존성을 외부에서 주입받는 것
- **Bean**: Spring Container가 관리하는 객체
- **BeanFactory**: 기본적인 IoC Container 인터페이스
- **ApplicationContext**: BeanFactory를 확장한 인터페이스
- **Configuration Metadata**: Bean 생성 및 의존 관계 설정 정보
- **Setter Injection**: `<property>` 태그를 이용한 의존성 주입
- **Constructor Injection**: `<constructor-arg>` 태그를 이용한 의존성 주입
- **Singleton**: 동일한 Bean을 조회하면 같은 객체 반환
- **Prototype**: Bean을 조회할 때마다 새로운 객체 생성

