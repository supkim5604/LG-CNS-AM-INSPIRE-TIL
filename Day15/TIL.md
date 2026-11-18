# [Day 15] LG CNS AM Inspire Camp 7기 TIL

작성일: 2026-11-18
<br>
과목: BE

## 오늘 학습한 주제

- 다형성(Polymorphism)

## 오늘 배운 것

### &#x20;다형성이란?

- 다형성(Polymorphism)은 하나의 객체가 여러 가지 타입으로 다뤄질 수 있는 객체지향 프로그래밍(OOP)의 특징이다.
- Java에서는 상속 관계에 있는 부모 클래스 타입의 참조 변수로 자식 클래스의 객체를 참조할 수 있다.
- 동일한 메서드를 호출하더라도 실제 객체의 종류에 따라 서로 다른 동작을 수행할 수 있다.

### 업캐스팅(Upcasting)

```java
class Animal {
    void sound() {
        System.out.println("동물 소리");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("멍멍");
    }
}

class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("야옹");
    }
}
```

```java
Animal animal1 = new Dog();
Animal animal2 = new Cat();

animal1.sound(); // 멍멍
animal2.sound(); // 야옹
```

- `Animal animal1 = new Dog()`처럼 자식 객체를 부모 타입의 참조 변수에 할당하는 것을 업캐스팅이라고 한다.
- `animal1`의 참조 변수 타입은 `Animal`이지만, 실제 객체는 `Dog`이다.
- 따라서 `sound()`를 호출하면 실제 객체인 `Dog`에서 오버라이딩한 메서드가 실행된다.

### 동적 메서드 디스패치(Dynamic Method Dispatch)

- Java에서는 오버라이딩된 인스턴스 메서드를 호출할 때 실제 객체의 타입을 기준으로 실행할 메서드를 결정한다.
- 이를 동적 메서드 디스패치라고 한다.

```java
Animal animal = new Dog();
animal.sound(); // 멍멍
```

- 컴파일 시점에는 참조 변수 타입인 `Animal`을 기준으로 메서드를 호출할 수 있는지 확인한다.
- 실행 시점에는 실제 객체인 `Dog`의 `sound()` 메서드가 실행된다.

### 다형성의 장점

- **코드 재사용성:** 부모 타입을 이용하여 여러 종류의 자식 객체를 처리할 수 있다.
- **유지보수성:** 새로운 자식 클래스를 추가하더라도 기존 코드를 수정할 필요가 줄어든다.
- **확장성:** 공통된 인터페이스를 통해 다양한 객체를 유연하게 관리할 수 있다.

## 내일 계획 & 아직 모르는 것

- 대학에서 배운 내용들을 다시 떠올려보는 시간을 가진것 같다. 내일부터는 springframework를 본격적으로 공부할 예정이다.
