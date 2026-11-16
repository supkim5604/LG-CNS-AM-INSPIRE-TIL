# [Day 13] LG CNS AM Inspire Camp 7기 TIL

작성일: 2026-11-16
<br>
과목: BE

## 오늘 학습한 주제
- Java 생성자(Constructor)
- 기본 생성자와 매개변수가 있는 생성자
- 생성자 오버로딩(Constructor Overloading)

## 오늘 배운 것
- 오늘은 백엔드 첫 수업이었다. 전체적인 개발환경 세팅과 자바의 기본적인 OOP개념에 대해서 배웠다. 그중에서 기본생성자와 인자를 받는 생성자에 대해 배웠다. 학교에서 배운 내용
  이었지만 다시 한번 리마인드 할 수 있는 좋은 시간이었다.

### 1. 생성자(Constructor)
- 생성자는 객체가 생성될 때 호출되며, 객체의 초기값을 설정하는 역할을 한다.
- 생성자 이름은 클래스 이름과 같아야 하며, 반환 타입을 작성하지 않는다.
- `new` 키워드로 객체를 생성할 때 호출된다.

### 2. 기본 생성자(Default Constructor)

```java
public MyDate() {
    System.out.println("Default Constructor가 호출됨!!");
}
```

```java
MyDate date = new MyDate();
```

- 매개변수가 없는 생성자이다.
- 생성자를 하나도 정의하지 않으면 컴파일러가 기본 생성자를 자동으로 제공한다.
- 단, 매개변수가 있는 생성자라도 직접 정의하면 기본 생성자는 자동으로 생성되지 않는다.
- 위 코드에서는 기본 생성자를 직접 정의했기 때문에 객체를 생성하면 메시지가 출력된다.
- 필드를 초기화하지 않았으므로 `int` 타입인 `year`, `month`, `day`의 초기값은 모두 `0`이다.

### 3. 매개변수가 있는 생성자

```java
public MyDate(int year, int month, int day) {
    this.year = year;
    setMonth(month);
    this.day = day;
}
```

```java
MyDate date2 = new MyDate(2026, 13, 16);
```

- 객체를 생성하면서 원하는 초기값을 전달할 수 있다.
- `this.year`는 현재 객체의 필드를 의미하고, `year`는 생성자의 매개변수를 의미한다.
- `setMonth(month)`를 사용하여 월이 1~12 사이인지 검증하도록 했다.

```java
public void setMonth(int month) {
    if (month >= 1 && month <= 12) {
        this.month = month;
    } else {
        System.out.println("Month는 1~12 사이의 값만 가능합니다.");
    }
}
```

- `13`은 유효하지 않은 월이므로 `month`에 값이 저장되지 않고 기본값 `0`이 유지된다.

### 4. 생성자 오버로딩(Constructor Overloading)

- 하나의 클래스에 매개변수의 개수나 타입이 다른 생성자를 여러 개 정의하는 것을 의미한다.

```java
public MyDate() {
    System.out.println("Default Constructor가 호출됨!!");
}

public MyDate(int year, int month, int day) {
    this.year = year;
    setMonth(month);
    this.day = day;
}
```

- `new MyDate()`는 매개변수가 없는 생성자를 호출한다.
- `new MyDate(2026, 11, 16)`은 매개변수가 3개인 생성자를 호출한다.

## 실행 결과

```text
Default Constructor가 호출됨!!
Month는 1~12 사이의 값만 가능합니다.
0
31
Month는 1~12 사이의 값만 가능합니다.
0
16
```

## 정리
- 생성자는 객체 생성 시 초기화 작업을 수행한다.
- 기본 생성자는 매개변수가 없고, 매개변수가 있는 생성자는 객체 생성 시 초기값을 전달받는다.
- 생성자 오버로딩을 통해 다양한 방법으로 객체를 초기화할 수 있다.
- 생성자 내부에서도 Setter를 호출하여 입력값을 검증할 수 있다.
