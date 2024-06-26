4. 리플렉션에 대해 설명해 주세요.
리플렉션은 구체적인 클래스 타입을 알지 못하더라도 그 클래스의 메서드, 타입, 변수들에 접근할 수 있도록 해주는 자바 API를 말하며, 컴파일 시간이 아닌 실행 시간에 동적으로 특정 클래스의 정보를 접근하거나 수정할 수 있는 프로그래밍 기법이라 할 수 있다. 
4.1. 의미만 들어보면 리플렉션은 보안적인 문제가 있을 가능성이 있어보이는데, 실제로 그렇게 생각하시나요? 만약 그렇다면, 어떻게 방지할 수 있을까요? 
리플렉션은 매우 강력한 도구로, 제한 없이 사용하면 보안 문제를 일으킬 수 있다. 예를 들어, 리플렉션을 통해 보호된(ex: private) 필드나 메소드에 접근하거나, 보안 매커니즘을 우회하는 데 사용될 수 있다.

이러한 문제 방지를 위해 아래와 같은 조치를 취할 수 있다.

- 최소한의 권한 부여
- 코드 검사와 테스트, 리플렉션을 사용하는 부분에서 예기치 않은 동작이 발생하지 않도록 해야 한다.
- 보안 매니저 사용, Java는 SecurityManager라는 시스템을 제공한다. 이를 사용하면 애플리케이션의 보안 정책을 더 세밀하게 제어할 수 있다. 예를 들어, 특정 작업(예: 리플렉션을 사용한 접근)을 허용하거나 금지하는 등의 설정을 할 수 있다.
- 의존하는 라이브러리 검사, 외부 라이브러리가 리플렉션을 어떻게 사용하는지 알아보고, 필요하다면 그 라이브러리의 사용을 재고해야 한다.
4.2. 리플렉션을 언제 활용할 수 있을까요?
코드를 작성할 시점에는 어떤 타입의 클래스를 사용할지 모르지만, 런타임 시점에 지금 실행되고 있는 클래스를 가져와서 실행해야 하는 경우 사용된다.

- 클래스 정보 얻기, Class 객체를 통해 클래스 이름, 부모 클래스, 구현한 인터페이스, 사용된 어노테이션 등의 정보를 얻을 수 있다.
- 메소드와 필드 정보 얻기, Method, Field, Constructor 등의 클래스를 사용하여 메소드, 필드, 생성자의 정보를 얻을 수 있다. 이들을 통해 메소드나 생성자를 호출하거나, 필드의 값을 읽거나 변경할 수도 있다.
- 동적 클래스 로딩, Class.forName() 메소드를 사용하여 문자열로 된 클래스 이름을 가지고 해당 클래스를 동적으로 로딩할 수 있다.
프레임워크나 IDE에서 이런 동적인 바인딩을 이용한 기능을 제공한다. intelliJ의 자동완성 기능, 스프링의 어노테이션이 리플렉션을 이용한 기능이라 할 수 있다.
11. IoC와 DI에 대해 설명해 주세요.
IoC, 프로그램의 제어 흐름을 직접 제어하는 것이 아니라 외부에서 관리하는 것이다.
DI, 애플리케이션 실행 시점(런타임)에 외부에서 실제 구현 객체를 생성하고 클라이언트에 전달해서 클라이언트와 서버의 실제 의존관계 연결한다.
11.1. 후보 없이 특정 기능을 하는 클래스가 딱 한 개하면, 구체 클래스를 그냥 사용해도 되지 않나요? 그럼에도 불구하고 왜 Spring에선 Bean을 사용 할까요?
객체 생성과 의존관계 연결을 스프링 컨테이너에게 넘겨줌으로써 확장과 변경에 유연한 프로그램을 만들 수 있다. 또한 객체를 싱글톤으로 관리해줌으로써 성능상 이점이 있다.
11.2. Spring의 Bean 생성 주기에 대해 설명해 주세요.
스프링 컨테이너 생성 -> 스프링 빈 생성 -> 의존성 주입 -> 초기화 콜백 : 빈이 생성되고, 빈의 의존관계 주입이 완료된 후 호출 -> 사용 -> 소멸전 콜백 :빈이 소멸되기 직전에 호출 -> 스프링 종료
11.3. 프로토타입 빈은 무엇인가요? 
- 싱글톤 : 디폴트 스코프. 스프링 컨테이너의 시작과 종료까지 유지되는 가장 넓은 범위의 스코프이다.
- 프로토타입 : 스프링 컨테이너는 프로토타입 빈의 생성과 의존 관계 주입까지만 관여하고, 더는 관리하지 않는 매우 짧은 범위의 스코프이다. 따라서 종료 메서드는 호출되지 않는다.
- 웹 관련 스코프
  - request : 웹 요청이 들어오고 나갈 때까지 유지되는 스코프이다.
  - session : 웹 세션이 생성되고 종료될 때까지 유지되는 스코프이다.
  - application : 웹의 서블릿 컨텍스트와 같은 범위로 유지되는 스코프이다.
12. AOP에 대해 설명해 주세요.
AOP는 Aspect Oriented Programming의 약자로 관점 지향 프로그래밍이라고 불린다. 관점 지향은 쉽게 말해 어떤 로직을 기준으로 핵심적인 관점, 부가적인 관점으로 나누어서 보고 그 관점을 기준으로 각모듈화하겠다는 것이다. 여기서 모듈화란 어떤 공통된 로직이나 기능을 하나의 단위로 묶는 것을 말한다.
AOP에서 각 관점을 기준으로 로직을 모듈화한다는 것은 코드들을 부분적으로 나누어서 모듈화하겠다는 의미다. 이때, 소스 코드상에서 다른 부분에 계속 반복해서 쓰는 코드들을 발견할 수 있는 데 이것을 흩어진 관심사 (Crosscutting Concerns)라 부른다.
위와 같이 흩어진 관심사를 Aspect로 모듈화하고 핵심적인 비즈니스 로직에서 분리하여 재사용하겠다는 것이 AOP의 취지다. 
12.1. @Aspect는 어떻게 동작하나요?
부가기능을 정의한 코드인 어드바이스(Advice)와 어드바이스를 어디에 적용하지를 결정하는 포인트컷(PointCut)을 합친 개념이다.
AOP 개념을 적용하면 핵심기능 코드 사이에 침투된 부가기능을 독립적인 애스펙트로 구분해 낼수 있다. 구분된 부가기능 애스펙트를 런타임 시에 필요한 위치에 동적으로 참여하게 할 수 있다.
15. JPA와 같은 ORM을 사용하는 이유가 무엇인가요?
객체와 관계형 DB의 패러다임 불일치를 극복하고자 
객체와 관계형 DB의 패러다임의 차이로 인해 객체지향적인 프로그래밍을 하지못하고 DB에 종속적인 개발을 하게된다. 이러한 문제를 해결하기 위해 JAVA진영에서는 JPA를 제공한다.
JPA가 쿼리문을 작성해주기 때문에 JPA를 통해 개발자는 더이상 쿼리문을 반복적으로 작성하거나 유지보수하는 것을 신경쓰지 않아도 된다.
그리고 JPA가 내부적으로 맵핑해주기 때문에 SQL 중심적인 개발에서 벗어나 객체지향적인 개발을 할 수 있게 된다.
15.1 영속성은 어떤 기능을 하나요? 이게 진짜 성능 향상에 큰 도움이 되나요?
Entity를 영구적으로 저장하는 환경이다.
- 1차 캐시
  - key : @Id , value : Entity로 저장
  - 조회 시 1차 캐시에서 먼저 찾음 → 1차 캐시에 없으면 DB에서 조회 → 1차 캐시에 저장 → 반환
- 영속 엔티티의 동일성 보장
    - 1차 캐시로 반복 가능한 읽기(Reapeatable read) 등급의 트랜잭션 격리 수준을 데이터베이스가 아닌 애플리케이션 차원에서 제공
    - 같은 트랜잭션 내에서 동일성 보장
- 쓰기 지연
    - 성능 최적화 여지 생김 → batch size를 주고 한 번에 batch size만큼의 쿼리를 보냄.
- 변경 감지 (Dirty Checking)
    - flush() → 엔티티와 스냅샷 비교 → 쓰기 지연 SQL 저장소에 UPDATE 쿼리 생성 → flush : 쿼리 날림 → commit
    - 스냅샷 : DB에서 최초로 값을 읽어온 시점의 스냅샷
- 지연 로딩
15.2 N + 1 문제에 대해 설명해 주세요.

16. @Transactional 은 어떤 기능을 하나요?

16.1. @Transactional(readonly=true) 는 어떤 기능인가요? 이게 도움이 되나요?
- 읽기 전용 트랜잭션
- 다양한 최적화 가능
- 프레임워크
    - JPA에선 커밋 시점에 플러스 호출 ❌
    - 변경 감지를 위한 스냅샷 생성 ❌
- JDBC Driver
    - 읽기 전용 트랜잭션에서 변경 쿼리 발생하면 예외 던짐
    - 읽기(슬레이브), 쓰기(마스터) 데이터베이스를 구분해서 요청
- 데이터베이스
    - 내부에서 성능 최적화
16.2. 그런데, 읽기에 트랜잭션을 걸 필요가 있나요? @Transactional을 안 붙이면 되는거 아닐까요? 

17. Java 에서 Annotation 은 어떤 기능을 하나요?
자바에서 어노테이션(Annotation)은 코드에 대한 메타데이터를 제공하는 방법이다. 
이는 컴파일러에게 코드 작성 방법을 알려주거나, 컴파일 시간 및 실행 시간에 해석될 수 있는 정보를 제공한다.
어노테이션은 자바 5부터 도입되었으며, 기존의 코드에 대한 정보를 추가하는 데 사용된다. 
왜냐하면 어노테이션을 통해 코드의 의도를 명확히 할 수 있고, 오류 가능성을 줄일 수 있기 때문이다.
17.1. 별 기능이 없는 것 같은데, 어떻게 Spring 에서는 Annotation 이 그렇게 많은 기능을 하는 걸까요?

17.2. Lombok의 @Data를 잘 사용하지 않는 이유는 무엇일까요?
Data 어노테이션은 @ToString, @EqualsAndHashCode, @Getter, @Setter, @RequiredArgsConstructor가 모두 포함되어 있다.
QueryDSL