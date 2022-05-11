<h1>common dbcp thread lock 에러</h1>
환경:네이버클라우드 , WISEU-LTS , 티베로6

티베로와 common dbcp의 조합은 내가 경험했던 DBCP 조합 중 가장 최악이었다.
이슈발생: DBCP에서 getconntion(커넥션풀을 꺼내오는과정) 중 지연이 발생하면 timeout에러를 뱉지 못하고 dbcp 스레드(싱글스레드)를 lock 하고 있어
다른 쓰레드에서 dbcp 호출 시 getconnetion 을 기다리며 스레드 lock을 발생시킴

트러블슈팅 내용들:
1.DBCP 2버전의 버그로 생각하여 DBCP 1 버전으로 다운그레이드 진행했으나 실패
2.DBCP 옵션인 MAX WAIT에 옵션을 주었으나 실패
3.티베로에서 가이드하는 read timeout 옵션을 주어 일정 시간이 지나면 timeout 에러를 발생시키며 lock 해제를 시켜줘야된다.
-> 그러나 티베로 DB에서 READ TIMEOUT은 정상적(?)으로 작동을 하지않는것 같다.  
(https://technet.tmaxsoft.com/upload/download/online/tibero/pver-20160406-000002/tibero_jdbc/ch03.html)
재현을 위해 READTIMEOUT을 강제로 발생시키고자 하였지만 방법을 찾지못했다..
DBCP 소스 자체에서 문제가 있을수도 있다고 생각이든다.

