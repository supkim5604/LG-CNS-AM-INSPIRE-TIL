# LG CNS AM Inspire Camp 7기 TIL

작성일: 2026-11-24  
과목: Spring Boot

## 오늘 학습한 주제

- @SpringBootApplication
- 명령줄 옵션을 for문, 람다식, 메서드 참조

## 오늘 배운 것

### @SpringBootApplication

Spring Boot의 시작 클래스에 `@SpringBootApplication`을 붙이면 세 가지 설정을 한 번에 적용할 수 있다.

- `@SpringBootConfiguration`은 이 클래스가 Spring 설정 클래스라는 뜻이다. 안에 `@Configuration`이 붙어 있다.
- `@ComponentScan`은 시작 클래스가 있는 패키지와 그 아래에서 `@Component` 등이 붙은 클래스를 찾아 Bean으로 등록한다.
- `@EnableAutoConfiguration`은 프로젝트에 추가한 라이브러리 등을 보고 필요한 설정을 자동으로 적용한다.

### 옵션 이름을 출력하는 세 가지 방법

프로그램을 실행할 때 `--port=8080`을 넘기면 `args.getOptionNames()`로 옵션 이름인 `port`를 얻을 수 있다. 아래 세 방법은 각각 `port`를 한 줄 출력한다.

```java
Set<String> optionNames = args.getOptionNames();

// for문
for (String name : optionNames) {
    System.out.println(name);
}

// 람다식
optionNames.forEach(name -> System.out.println(name));

// 메서드 참조
optionNames.forEach(System.out::println);
```

`forEach`에는 이름 하나를 꺼낼 때마다 할 일을 넘겨준다. 자바에서는 이런 일을 맡는 인터페이스를 `Consumer`라고 하고, 그 일을 실행하는 메서드가 `accept()`다.

람다식 `name -> System.out.println(name)`은 ‘이름 하나를 받아 출력해’라는 뜻이다. 받은 이름을 그대로 `println`에 넘기기 때문에 메서드 참조인 `System.out::println`으로 더 짧게 쓸 수 있다.

## 어려웠던 점 & 해결 과정

처음에는 `getOptionNames()`가 환경변수를 읽는 줄 알았다. `--port=8080`처럼 프로그램을 실행할 때 직접 넘긴 옵션의 이름을 읽는다고 정리했다.

`name = port`처럼 앞에 문구를 붙이고 싶을 때는 `name -> System.out.println("name = " + name)`처럼 람다식에 출력할 내용을 적으면 된다.


