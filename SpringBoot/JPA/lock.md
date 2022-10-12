# 잠금(Lock)의 종류
## 낙관적 잠금(Optimisstic Lock)
낙관적 잠금은 현실적으로 데이터 갱신시 경합이 발생하지 않을 것이라고 낙관적으로 보고 잠금을 거는 기법입니다. 
락이 걸리지 않는 도메인이라고 생각하면 사용함
이는 엄밀한 의미에서 보면 잠금이라기 보다는 일종의 충돌감지(Conflict detection)에 가깝습니다.

## 비관적 잠금(Pessimistic Lock)
동일한 데이터를 동시에 수정할 가능성이 높다는 비관적인 전제로 잠금을 거는 방식입니다. 
예를 들어 상품의 재고는 동시에 같은 상품을 여러명이 주문할 수 있으므로 데이터 수정에 의한 경합이 발생할 가능성이 높다고 비관적으로 보는 것입니다.
이 경우 충돌감지를 통해서 잠금을 발생시키면 충돌발생에 의한 예외가 자주 발생하게 됩니다. 
이럴경우 비관적 잠금을 통해서 예외를 발생시키지 않고 정합성을 보장하는 것이 가능합니다. 
다만 성능적인 측면은 손실을 감수해야 합니다. 주로 데이터베이스에서 제공하는 배타잠금(Exclusive Lock)을 사용합니다.
 ```
   @Lock(value = LockModeType.PESSIMISTIC_WRITE)
    @Query("select s from Stock s where s.id=:id")
    Stock findByIdWithPessimisticLock(Long id);
```
 
## 암시적 잠금(Implicit Lock)
암시적 잠금은 프로그램 코드상에 명시적으로 지정하지 않아도 잠금이 발생하는 것을 의미합니다. 
JPA에서는 엔터티에 @Version이 붙은 필드가 존재하거나 @OptimisticLocking 어노테이션이 설정되어 있을 경우 자동적으로 충돌감지를 위한 잠금이 실행됩니다. 
그리고 데이터베이스의 경우에는 일반적으로 사용하는 대부분의 데이터베이스가 업데이트, 삭제 쿼리 발행시에 암시적으로 
해당 로우에 대한 행 배타잠금(Row Exclusive Lock)이 실행됩니다. 
JPA의 충돌감지가 역할을 할 수 있는 것도 이와 같은 데이터베이스의 암시적 잠금이 존재하기 때문입니다. 
데이터베이스의 암시적 잠금이 없다면 충돌감지를 통과한 후 커밋(Commit)이 실행되는 사이에 틈이 생기므로 충돌감지를 하더라도 정합성을 보증할 수 없을 것입니다.


그리고 버전은 Integer 뿐만 아니라 Long, Short 등 다양한 Number가 가능합니다. 그리고 Timestamp 자료형 또한 사용할 수 있습니다.


## 명시적 잠금(Explicit Lock)
프로그램을 통해 의도적으로 잠금을 실행하는 것이 명시적 잠금입니다. JPA에서 엔터티를 조회할 때 LockMode를 지정하거나 
select for update 쿼리를 통해서 직접 잠금을 지정할 수 있습니다.
 
## JPA에서는 @Version 어노테이션이 붙여서 낙관적락 구현 
update를 하기전에 버전이 적절한지 체크하도록 합니다. 
만약 조회했을 때와 업데이트를 할때 버전이 맞지 않는다면 OptimisticLockException를 예외로 throw 하게됩니다. 
그리고 업데이트가 성공할경우 version을 올리게됩니다.
```

    @Version
    private Long version;
```

# LockMode 종류
적용방법
``` 
@Transactional
@Lock(value = LockModeType.PESSIMISTIC_WRITE) //여기
public int decreasePrice(String name, int price)
``` 

## LockModeType.PESSIMISTIC_WRITE
일반적인 옵션. 데이터베이스에 쓰기 락
다른 트랜잭션에서 읽기도 쓰기도 못함. (배타적 잠금)

## LockModeType.PESSIMISTIC_READ
반복 읽기만하고 수정하지 않는 용도로 락을 걸 때 사용
다른 트랜잭션에서 읽기는 가능함. (공유 잠금)

## LockModeType.PESSINISTIC_FORCE_INCREMENT
Version 정보를 사용하는 비관적 락


 
