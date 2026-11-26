# LG CNS AM Inspire Camp 7기 TIL

작성일: 2026-11-26  
과목: BE

## 오늘 학습한 주제

- `spring.jpa.hibernate.ddl-auto`의 `create`, `update`, `validate`
- `spring.jpa.show-sql`로 Hibernate가 실행하는 SQL을 확인하는 방법

## 오늘 배운 것

`ddl-auto`는 Spring Boot 애플리케이션에서 Hibernate가 엔티티 매핑을 기준으로 데이터베이스 구조를 어떻게 처리할지 정하는 설정이다. 이번 실습에서는 Spring Boot 애플리케이션을 MariaDB에 연결했다. `application.properties`에서 값을 하나 선택한다.

| 설정 | 애플리케이션 시작 시 동작 | 기존 데이터 |
| --- | --- | --- |
| `create` | 엔티티에 매핑된 테이블을 삭제하고 다시 생성한다. | 삭제된 테이블의 데이터도 사라진다. |
| `update` | 기존 스키마와 엔티티 매핑을 비교하고, 누락된 컬럼 추가처럼 지원되는 변경을 반영한다. | 컬럼 추가 같은 변경에서는 기존 행이 유지된다. |
| `validate` | 엔티티 매핑에 필요한 테이블과 컬럼이 있는지, 컬럼 타입이 맞는지 검사한다. | 스키마와 데이터가 그대로 유지된다. |


### MariaDB 연결과 JPA 설정

실습에서는 MariaDB에 `boot_db`를 만든 뒤 `boot` 계정으로 연결했다. 아래는 실습에서 사용한 속성이다.

```properties
myboot.age=${random.int(51,100)}
myboot.fullName=PROD ${myboot.name} Boot

logging.level.com.inspirecamp7.myspringbootproject4=INFO

spring.datasource.url=jdbc:mariadb://${DB_HOST:127.0.0.1}:${DB_PORT:3306}/${DB_DATABASE:boot_db}
spring.datasource.username=${DB_USERNAME:boot}
spring.datasource.password=${DB_PASSWORD}
spring.datasource.driverClassName=org.mariadb.jdbc.Driver

spring.jpa.hibernate.ddl-auto=validate
spring.jpa.show-sql=true
spring.jpa.database-platform=org.hibernate.dialect.MariaDBDialect
```

- `${이름:기본값}`은 해당 설정값이 없으면 기본값을 사용한다. 위 설정의 기본 접속 대상은 `127.0.0.1:3306/boot_db`이고, 기본 사용자 이름은 `boot`다. 비밀번호는 `DB_PASSWORD`로 전달한다.
- `org.mariadb.jdbc.Driver`는 MariaDB에 연결하는 JDBC 드라이버다. `MariaDBDialect`는 Hibernate가 MariaDB에 맞는 SQL을 생성하는 데 사용한다.
- `myboot.age`는 51 이상 100 미만의 정수를 사용하고, `myboot.fullName`의 `${myboot.name}`은 해당 속성값으로 치환된다. 프로젝트 패키지의 로그 레벨은 `INFO`다. 
- `spring.jpa.show-sql=true`로 Hibernate가 실행하는 SQL을 콘솔에서 확인할 수 있다. 

### customers 테이블에서 세 옵션 비교하기

같은 MariaDB에 연결한 채 `spring.jpa.hibernate.ddl-auto`의 값만 바꾸어 비교한다. 엔티티가 `customer_address` 컬럼을 매핑하고, DB에는 주소 컬럼이 없는 `customers` 테이블과 기존 고객 데이터가 있다고 가정한다.

- **`validate`**로 시작하면 Hibernate가 `customer_address` 누락을 감지해 앱 시작이 실패한다. 테이블이 아예 없어도 시작이 실패한다.
- **`create`**로 시작하면 Hibernate가 `customers` 테이블을 삭제하고 주소 컬럼을 포함해 다시 만든다. 기존 고객 행도 삭제된다.
- **`update`**로 시작하면 Hibernate가 기존 `customers` 테이블에 주소 컬럼을 추가할 수 있다. 기본값 없는 nullable 컬럼이 추가되면 기존 고객 행은 유지되고 주소는 `NULL`이다. 컬럼 이름 변경과 데이터 이전에는 별도의 마이그레이션이 필요하다.

### MariaDB 콘솔에서 확인한 결과

첨부한 실습 기록에서 `DESC customers`로 컬럼 구조를, `SELECT * FROM customers`로 기존 행을 확인했다. 처음에는 컬럼이 4개였고, 이후 `customer_address`가 추가되어 5개가 됐다. 조회 결과에는 기존 고객 2명이 남아 있었고 두 행의 주소는 모두 `NULL`이었다. 이 결과는 위 `update` 예시와 일치한다.

실습 중에는 콘솔에서 `DROP TABLE customers`도 직접 실행했다. 테이블을 삭제한 뒤 마지막 조회에서는 MariaDB의 `ERROR 1146`이 출력됐다.

