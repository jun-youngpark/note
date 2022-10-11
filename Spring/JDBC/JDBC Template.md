# JdbcTemplate

1. JdbcTemplate
 
스프링에서는 jdbcTemplate 객체를 사용하여 query, update 처리 시 기본적으로 작업해 주어야할
jdbc 커넥션 정보와 Statement, PreparedStatment 객체에 대한 작업들을 처리해 준다.
 
jdbcTemplate 에서는 콜백과 템플릿을 사용하고 있는데,
콜백은 특정 메소드를 실행하기 위하여 메소드를 담고 있는 객체를 통채로 전달하는 것을 말하고,
템플릿은 변하지 않는 부분과 변하는 부분을 구분하여, 변하는 부분에 원하는 로직을 넣을수 잇도록 템플릿화 해 놓은 것이라고 할수 있다.
 
jdbcTemplate 에서는 쿼리와 바인딩 파라미터를 콜백으로 던지고, 나머지 부분인 커넥션 관련 부분은 템플릿에 맡긴다.
다시말하면, 변하는 부분인 쿼리 부분만, 콜백으로 던지고, 변하지 않는 부분인 커넥션 연결, 반환 부분은 템플릿으로 미리 정의한데로 사용하는 것이다.
 
 
 
 
2. JdbcTemplate & Transaction
 
미리 생성되어 TransactionSynchronizationManager 를 통하여 트렌젝션 동기화 저장소에 등록된 커넥션 객체가 있으면 가져다가 재활용하고, 없을 경우 새로운 커넥션을 생성한다.
 
트랜젝션 처리가 필요없을 경우 JdbcTemplate 를 사용하면 되고, 트랜젝션 처리가 필요할 경우에는 tracactionSynchronazationManager 를 생성하고 JdbcTemplate 를 사용하면 된다.
 
 
 
3. 로컬 트랜젝션과 글로벌 트랜젝션
 
기본적은 JdbcTemplate 는 1개의 db 에 대한 작업을 담당하게 되고 1개의 db에 대하여 2번의 방법으로 트랜젝션을 수행하는것을 로컬 트랜젝션이라고 한다,
 
그러나 애플리케이션에서 2개 이상의 dbms 의 트랜젝션을 요구할 경우 우리는 글로벌 트랜젝션을 고려해야한다,
 
예를 들어 오라클과 mysql 2개의 dbms 에 대한 트랜젝션 처리가 필요할 경우가 있겠다.
 
 
 
스프링에서는 글로벌 트랜젝션 처리를 위하여 JTA (Java Transaction API ) 를 제공하고 있다.
 
JTA 를 사용하게 되면 애플리케이션은 쿼리, 업데이트 , 메시징들의 작업은 기존의 Jdbc 나 jms 를 사용하여 처리하고 트랜젝션 처리의 경우에는 JTA 가 처리하도록 위임하게 된다.
 
다시 말하자면, 트랜젝션이 아닌 작업의 경우에는 리소스를 JDBC나 JMS 가 담당하지만, 트랜젝션 작업의 경우에는 JTA 가 리소스와 직접 XA 통신으로 처리하는 작업을 수행하는 것이다.
 
 
4. PlatformTransactionManager 사용하기
 
PlatformTransactionManager 인터페이스를 상속한 객체
 
DatasouceTransactionManager 와 JTATransactionManager 를 사용하면 된다.
 
 
1) 로컬 트랜젝션
 
DatasouceTransactionManager 객체를 통하여 트랜젝션을 처리하게 되는데. 1개의 datasource 에 대한 트렌젝션 처리를 담당한다.
 
DatasouceTransactionManager 객체를 생성하고 getTransaction() 메소드를 호출하면, 트렌젹션은 시작되고,
트렌젝션의 상태는 TransactionStatus 타입의 변수에 저장된다.
 
public void update(){
    PlatformTransactionManager txm = new  DatasouceTransactionManager(datasource);
     
    //트렌젝션 시작
    TransactionStatis txs = txm.getTransaction(new DefaultTransactionDfinition());
 
    try{
            //업데이트 처리
           tmx,commit(txs);
    }catch {
           tmx.rollback(txs);
    }
}
 
 
2) 글로벌 트랜젝션 
 
글로벌 트렌젝션의 경우에는 JTATranactionManager 를 사용하면 되는데, 
주요 자바에서 사용하는 jta 정보를 JNDI를 통해 자동으로 인식하는 기능을 가지고 있어 별도의 datasource 를 지정하지 않아도 된다.
 
위의 로컬 트랜젝션에서
PlatformTransactionManager txm = new  JTATranactionManager();
부분만 변경해 주면 된다.
 
 
 
 
5. AOP 를 사용한 트렌젹션 처리
 
어드바이저 : 포인트컷 + 어드바이스
 
@Transactional
메소드, 클래스, 인터페이스에 적용할 수 있다.
 
스프링은  @Transactional 어노테이션을 지정하면 자동으로 TransactionAtrributeSourcePointcut 포인트 컷에 의하여,
트랜잭션 처리 대상으로 선정한다.
 
포인트 컷에 의하여 선정된 메소드, 객체는 TransactionIntercepter (어드바이스) 에 의하여 처리된다.
이때 TransactionIntercepter 는AnnotationTrasactionAttributeSource 를 사용하여 @Transactional 어노테이션에 설정한 정보를 참조하여 트렌젝션 처리를 수행한다.
 
@Transactional 어노테이션에서 설정할 수 있는 세부설정 값은 아래와 같다
 
@Target({ElementType.METHOD, ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Inherited
@Documented
public @interface Transactional {

 String value() default "";
 
 Propagation propagation() default Propagation.REQUIRED;

 Isolation isolation() default Isolation.DEFAULT;

 int timeout() default TransactionDefinition.TIMEOUT_DEFAULT;
 
 boolean readOnly() default false;

 Class<? extends Throwable>[] rollbackFor() default {};

 String[] rollbackForClassName() default {};
 
 Class<? extends Throwable>[] noRollbackFor() default {};
 
 String[] noRollbackForClassName() default {};
}
 
 
@Transactional 어노테이션은 가자 작은 단위인 메소드 단위부터 적용여부를 판단한다,
 
메소드에 있는지 여부 확인 -> 클래스에 있는지 여부 확인 -> 해당 클래스의 인터페이스에 있는 지 여부 확인
또한 클래스와 메소드에 모두 어노테이션이 설정되어 있다면 더 세부 단위의 설정을 우선순위로 한다.
 
클래스와 메소드 중 메소드의 어노테이션 설정에 따라 해당 메소드는 트랜젝션을 처리하는 것이다.
 
 
 
그럼 스프핑에서 @Transactional 어노테이션 기반으로 트랜젝션을 처리하도록 하려면 어떻게 해야할까?
 
Application-context.xml 에 아래와 같이 설정하면 된다.
 
<tx:annotation-driven />
 
 
 
6. 트렌젝션 전파
 
PROPAGATION_REQUIRED
가장 많이 사용하는 전파 속성으로, 진행중인 트랜잭션이 없으면 새로 시작하고, 이미 시작된 트렌젝션이 있으면 이에 참여한다.
 
PROPAGATION_REQUIRES_NEW
항상 새로운 트렌젝션을 시작한다. 독립적인 트렌젝션이 보장되어야 하는 경우 사용한다.
 
PROPAGATION_NOT_SUPPORTED
트렌잭션없이 동작한다. 특정한 메소드에만 트랜젝션을 제외하고 싶은 경우 사용가능하다.
 
 
 
트렌젝션 전파는 트렌젝션 메니저에서 트렌젝션 스테이터스를 가져와 적용하는 시점에 설정가능하다.
 
TransactionStatus status = this.transactionManager.getTransaction(이부분);
//TransactionStatus status = this.transactionManager.getTransaction(new DefaultTransactionDefinition());
this.transactionManager.commit(status);
this.transactionManager.rollback(status);
 
 
 
 
7. 격리수준
 
여러개의 트렌젝션이 동시에 실행되는 경우가 서비스 에서는 비번할것이다.
이경우 어떻게 데이터의 무결성을 가져갈 것인가를 결정하게 되는데, 이를 격리 수준이라고한다.
 
격리수준은 각  DBMS 별로 설정이 가능하고, 스프링 기본 값은 ISOLATION_DEFAULT 이다.
이것은 DB나 datasource 에 설정된 격리수준을 사용하겠다는 의미이다
 
 
 
8. 트렌젝션 타임아웃
 
각 트렌젝션의 타임아웃을 설정할 수 있다.
DefaultTransactionDefination 의 기본설정은 제한 시간 없음이다.
이럴경우 일부 슬로우 쿼리에 의하여 DBMS 와의 커넥션이 다 찼을 경우 전면 장애로 이어질 수 있으니, 슬로우 쿼리 일부는 타이아웃 설정에 의하여 제한 될 수 있도록 설정해 주는 것이 좋다.
 
 
9. READ ONLY
 
읽기전용 설정으로 트렌젝션 처리를 제한할 수 도 있다.
 
 
 
* 애플리케이션에서 원할 경우 여러개의 트렌젝션 전략을 가져갈 수 있다.
<aop:config>
    <aop:advice advice-ref="A" pointcut="">
    <aop:advice advice-ref="B" pointcut="">
</aop:config>
 
<tx:advice id="A">
     <tx:attribute>
             설정내용
     </tx:attribute>
</tx:advice>
 
<tx:advice id="B">
     <tx:attribute>
             설정내용
     </tx:attribute>
</tx:advice>
 
 
또는 @transactional 를 사용하여 적용가능하다. transactional  어노테이션에서는 위의 어트리뷰트 설정이 다 있다
@transactional  어노테이션은 클래스, 인터페이스, 메소드에 설정가능하며,
스프링에서는 클래스 메소드-> 클래스 -> 인터페이스 메소드 -> 인터페이스 의 순서로 찾아나간다
보내기
이전글	
이클립스 서버 메모리 설정
다음글	
이제는 말할 수 있다 Spring3 - 테스트 만들기
'jdbctemplate'에 대한 카페검색글	더보기
이제는 말할 수 있다 Spring3 - JdbcTemplate , Transaction
