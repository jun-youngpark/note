# MYSQL LOCK 종류
MySQL에서 Lock은 크게 Table Lock, Global Lock, Name Lock, User Lock 이 있다.

* Table Lock

테이블락은 어떤 세션에서 테이블 자원에 엑세스하여 데이터를 읽거나 쓰기를 할때 다른 세션에서는 테이블 자원에 대한 엑세스를 제한 하는 락이다. 
세션에서 명시적으로 테이블 락을 사용하면 그 세션에서 락을 해지하지 않으면 다른 세션에서는 접근을 하지 못하게 된다.
테이블 락을 사용하기 위해서는 테이블 락 권한을 가지고 있어야 가능하다.


## MYSQL NAMED LOCK 이란?

