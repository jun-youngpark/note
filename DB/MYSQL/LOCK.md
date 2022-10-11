# MYSQL LOCK 종류
MySQL에서 Lock은 크게 Table Lock, Global Lock, Name Lock, User Lock 이 있다.

* Table Lock

테이블락은 어떤 세션에서 테이블 자원에 엑세스하여 데이터를 읽거나 쓰기를 할때 다른 세션에서는 테이블 자원에 대한 엑세스를 제한 하는 락이다. 
세션에서 명시적으로 테이블 락을 사용하면 그 세션에서 락을 해지하지 않으면 다른 세션에서는 접근을 하지 못하게 된다.
테이블 락을 사용하기 위해서는 테이블 락 권한을 가지고 있어야 가능하다.

* Global Lock
  정확하게 말하면 글로벌 리드 락 (Global Read Lock)이다. 현재 세션 자체에서 글로벌하게 READ LOCK을 사용할 때 flush tables 명령으로 사용할 수 있다.

```
FLUSH TABLES WITH READ LOCK;
```
* Name Lock
 GET_LOCK에 사용하는 name string과 이해하기에 혼동될 수 있다. 테이블은 이름을 변경하거 삭제될때 테이블 레벨에서 묵시적으로 네임 락을 사용한다. 만약 이미 WRITE 락이 걸려 있는 테이블을 삭제한다고 할때를 살펴보자.
 
 * User Lock
사용자 레벨에서 락을 걸수 있는 방법이 있는데 이 방법은 락의 이름과 그 락의 타임아웃을 정의해서 사용하는 방법이다. GET_LOCK(str, timeout)이라는 메소드를 사용하여 락을 만들고 다른 세션에서 이 락의 이름이 있는지를 확인하고 있을 경우 정해진 타임 아웃기간 동안 락을 걸 수 있다. 그리고 락을 해지하기 위해서는 RELEASE_LOCK(str)을 명령을 사용한다. 이 방법은 Advisory Locking이라고도 한다.

두개의 세션을 열고 하나의 세션에서 다음 문장을 실행해보자. ‘user_define_lock’이라는 락을 10초동안 유지하도록 하였다.

## MYSQL User Lock 
GET_LOCK(str,timeout)

입력받은 이름(str) 으로 timeout 초 동안 잠금 획득을 시도합니다. timeout 에 음수를 입력하면 잠금을 획득할 때까지 무한대로 대기하게 됩니다.
한 session에서 잠금을 유지하고 있는동안에는 다른 session에서 동일한 이름의 잠금을 획득 할 수 없습니다.
GET_LOCK() 을 이용하여 획득한 잠금은 Transaction 이 commit 되거나 rollback 되어도 해제되지 않습니다.
GET_LOCK() 의 결과값은 1, 0, null 을 반환합니다.
