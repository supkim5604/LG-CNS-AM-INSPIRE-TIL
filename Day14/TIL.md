# [Day 14] LG CNS AM Inspire Camp 7기 TIL

작성일: 2026-11-17
<br>
과목: BE

## 오늘 학습한 주제
- static과 non-static의 차이

## 오늘 배운 것

###  static (정적 멤버)

`static`은 클래스에 속하는 멤버를 의미한다. 객체를 생성하지 않아도 클래스 이름을 통해 접근할 수 있으며, 모든 객체가 동일한 static 변수를 공유한다.

```java
class Counter {
    static int count = 0;

    Counter() {
        count++;
    }
}

public class Main {
    public static void main(String[] args) {
        Counter c1 = new Counter();
        Counter c2 = new Counter();

        System.out.println(Counter.count); // 2
    }
}
```

- `count`는 객체마다 생성되는 변수가 아니라 클래스에 하나만 존재하는 변수이다.
- 객체를 생성할 때마다 `count`가 증가하므로 최종 결과는 2가 된다.

###  non-static (인스턴스 멤버)

non-static은 객체에 속하는 멤버를 의미한다. 객체를 생성해야 접근할 수 있으며, 각 객체는 자신의 인스턴스 변수를 가진다.

```java
class Counter {
    int count = 0;

    Counter() {
        count++;
    }
}

public class Main {
    public static void main(String[] args) {
        Counter c1 = new Counter();
        Counter c2 = new Counter();

        System.out.println(c1.count); // 1
        System.out.println(c2.count); // 1
    }
}
```

- `count`는 객체마다 별도로 존재한다.
- `c1`과 `c2`는 서로 다른 객체이므로 각각 자신의 `count`를 가진다.

### 3. static과 non-static 비교

| 구분 | static | non-static |
|---|---|---|
| 소속 | 클래스 | 객체(인스턴스) |
| 객체 생성 | 필요 없음 | 필요 |
| 변수 공유 | 모든 객체가 공유 | 객체마다 독립적 |
| 접근 방법 | `클래스명.멤버` | `객체명.멤버` |
| 대표 예시 | `Math.random()` | `list.add()` |

### 4. 주의 사항

static 메서드에서는 non-static 멤버에 직접 접근할 수 없다.

```java
class Example {
    int num = 10;

    static void print() {
        System.out.println(num); // 컴파일 오류
    }
}
```

`num`은 객체에 속하는 변수이지만 `print()`는 객체 없이 호출할 수 있는 static 메서드이기 때문이다.

접근하려면 객체를 생성해야 한다.

```java
static void print() {
    Example ex = new Example();
    System.out.println(ex.num); // 10
}
```

## 오늘 배운 점

static은 클래스에 속하며 객체들이 공유하는 데이터를 관리할 때 사용할 수 있고, non-static은 객체마다 독립적인 상태를 관리할 때 사용한다는 차이를 알게 되었다.

특히 static 메서드에서는 인스턴스 변수에 직접 접근할 수 없다는 점을 이해했다.
