# 아이템 1. 생성자 대신 static 팩토리 메소드를 고려해 볼 것

[![생성자 대신 static 팩토리 메소드를 고려해 볼 것](https://img.youtube.com/vi/X7RXP6EI-5E/0.jpg)](https://youtu.be/X7RXP6EI-5E)

```java
public static Boolean valueOf(boolean b) {
    return b ? Boolean.TRUE : Boolean.FALSE;
} 
```

public 생성자를 사용해서 객체를 생성하는 전통적인 방법 말고, 이렇게 public static 팩토리 메소드를 사용해서 해당 클래스의 인스턴스를 만드는 방법도 있다.

이런 방법에는 각각 장단점이 있는데 다음과 같다.

## 장점 1: 이름을 가질 수 있다.

생성자에 제공하는 파라메터가 거기서 반환하는 객체를 잘 설명하지 못할 경우에, 잘 만든 이름을 가진 static 팩토리를 사용하는 것이 사용하기 보다 더 쉽고 (해당 팩토리 메소드의 클라이언트 코드를) 읽기 편한다. 그 예로 `BigInteger.probblePrime`을 들고 있다.

또, 생성자는 시그니처에 제약이 있다. 똑같은 타입을 파라미터로 받는 생성자 두개를 만들 수 없으니까 그런 경우에도 public static 팩토리 메소드를 사용하는것이 유용하다.

## 장점 2: 반드시 새로운 객체를 만들 필요가 없다.

불변(immutable) 클래스([아이템 17](item17.md))인 경우나 매번 새로운 객체를 만들 필요가 없는 경우에 미리 만들어둔 인스턴스 또는 캐시해둔 인스턴스를 반환할 수 있다. `Boolean.valueOf(boolean)` 메소드도 그 경우에 해당한다.

```
    public static Foo withName(String name) {
        return new Foo(name);
    }
```
## 장점 3: 리턴 타입의 하위 타입 인스턴스를 만들 수도 있다.

클래스에서 만들어 줄 객체의 클래스를 선택하는 유연함이 있다.
리턴 타입의 하위 타입의 인스턴스를 만들어줘도 되니까, 리턴 타입은 인터페이스로 지정하고 그 인터페이스의 구현체는 API로 노출 시키지 않지만 그 구현체의 인스턴스를 만들어 줄 수 있다는 말이다. `java.util.Collections`가 그 예에 해당한다.

`java.util.Collections`는 45개에 달하는 인터페이스의 구현체의 인스턴스를 제공하지만 그 구현체들은 전부 non-public이다. 즉 인터페이스 뒤에 감쳐줘 있고 그럼으로서 public으로 제공해야 할 API를 줄였을 뿐 아니라 개념적인 무게(conceptual weight)까지 줄일 수 있었다.

여기서 개념적인 무게란, 프로그래머가 어떤 인터페이스가 제공하는 API를 사용할 때 알아야 할 개념의 개수와 난이도를 말한다.

그러한 팩토리를 사용하는 코드가 구현체가 아닌 인터페이스 타입으로 코딩하게 되는건 덤으로 좋은 일이다.

자바 8부터  인터페이스에 public static 메소드를 추가할 수 있게 되었지만 private static 메소드는 자바 9부터 추가할 수 있다. 따라서 자바 8부터 인터페이스에 public static 메소드를 사용해서 그 인터페이스의 구현체를 메소드를 제공할 수도 있지만 private static 메소드가 필요한 경우, 자바 9가 아니면 기존처럼 별도의 (인스턴스를 만들 수 없는, `java.util.Collections` 같은) 클래스를 사용해야 할 수도 있다. 

## 장점 4: 리턴하는 객체의 클래스가 입력 매개변수에 따라 매번 다를 수 있다.

장점 3과 같은 이유로 객체의 타입은 다를 수 있다. `EnumSet` 클래스 ([아이템 36](item36.md))는 생성자 없이 public static 메소드, `allOf()`, `of()` 등을 제공한다. 그 안에서 리턴하는 객체의 타입은 enum 타입의 개수에 따라 `RegularEnumSet` 또는 `JumboEnumSet`으로 달라진다.

그런 객체 타입은 노출하지 않고 감춰져 있기 때문에 추후에 JDK의 변화에 따라 새로운 타입을 만들거나 기존 타입을 없애도 문제가 되지 않는다.

## 장점 5: 리턴하는 객체의 클래스가 public static 팩토리 메소드를 작성할 시점에 반드시 존재하지 않아도 된다.

장점 3, 4와 비슷한 개념이다. 이러한 유연성을 제공하는 static 팩토리 메소드는 `서비스 프로바이더` 프레임워크의 근본이다. `JDBC`를 예로 들고 있다.

`서비스 프로바이더` 프레임워크는 서비스의 구현체를 대표하는 `서비스 인터페이스`와 구현체를 등록하는데 사용하는 `프로바이더 등록 API` 그리고 클라이언트가 해당 서비스의 인스턴스를 가져갈 때 사용하는 `서비스 엑세스 API`가 필수로 필요하다. 부가적으로, 서비스 인터페이스의 인스턴스를 제공하는 `서비스 프로바이더 인터페이스`를 만들 수도 있는데, 그게 없는 경우에는 리플랙션을 사용해서 구현체를 만들어 준다.

`JDBC`의 경우, `DriverManager.registerDriver()`가 `프로바이더 등록 API`. `DriverManager.getConnection()`이 `서비스 엑세스 API`. 그리고 `Driver`가 `서비스 프로바이더 인터페이스` 역할을 한다.

자바 6부터는 `java.util.ServiceLoader`라는 일반적인 용도의 서비스 프로바이더를 제공하지만, `JDBC`가 그 보다 이전에 만들어졌기 때문에 `JDBC`는 `ServiceLoader`를 사용하진 않는다.

## 단점 1: public 또는 protected 생성자 없이 static public 메소드만 제공하는 클래스는 상속할 수 없다.

따라서, `Collections 프레임워크`에서 제공하는 편의성 구현체(`java.util.Collections`)는 상속할 수 없다. 오히려 불변 타입([아이템 17](item17.md))인 경우나 상속 대신 컴포지션을 권장([아이템 18](item18.md))하기 때문에 장점이라 말할지도 모르겠다.

## 단점 2: 프로그래머가 static 팩토리 메소드를 찾는게 어렵다.

생성자는 Javadoc 상단에 모아서 보여주지만 static 팩토리 메소드는 API 문서에서 특별히 다뤄주지 않는다. 따라서 클래스나 인터페이스 문서 상단에 팩토리 메소드에 대한 문서를 제공하는 것이 좋겠다.

## 참고

* [ServiceLoader](https://docs.oracle.com/javase/9/docs/api/java/util/ServiceLoader.html)
