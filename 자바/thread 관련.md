#  쓰레드 ( Thread )
 
▶▶ 쓰레드 ( Thread )
프로세스 :  실행 중인 프로그램
data ( 값 )
code
thread ( 실행 흐름 )
         
* Thread  : 프로세스 내의 실행 흐름
프로세스 내의 code와 data를 이용해 program의 실행을 관리 
// 일반적으로 프로그램을 실행하게 되면, main() 함수가 실행되면서, 하나의 프로세스가 진행된다. 이런 하나의 프로  
세스를 메인 스레드라고 보면 되는데, 메인 스레드 하나만 있는 것을 싱글 스레드(single-thread) 라고 한다.

* Multi - Thread  : process 내의 여러 개의 Thread들 이 동시에 실행되는 것  
실행 중인 thread 들은 process 내의 code와 data를 공유할 수 있다. ( 무조건은 아님 )

※ Data 일관성 문제 발생 : 쓰레드의 가장 큰 문제점, 서로 data를 공유하여 사용하므로 data의 안전성에 문제가 있다.  

* Java의 Thread 코딩
main() → main Thread가 실행시킬 메소드
방법 종류

java.lang.Thread 를 extends
public void run() 메소드 오버라이딩 // main Thread의 main() 역할

Thread 로 실행
Thread 객체생성 → start()
TvThread t = new TvThread()
t.start()   // 새로운 쓰레드 실행

Java.lang.Runnable implements 하고 public void run() 메소드 overriding
// Thread가 실행할 코드 작성. 자체는 쓰레드가 아님 !  so 쓰레드의 인스턴스로 사용

Thread 로 실행
Runnable 객체 생성
Thread 객체 생성 → 1의 객체에 주입
Thread 객체.start()   // 새로운 쓰레드 실행

코드 예제 )    TvThread tvt = new TvThread()
Thread t = new Thread(tvt) 
t.start()


※ 실행 첫 순간에는 main 뿐, 병렬로 실행한다.


 
* 싱글쓰레드 vs 멀티 쓰레드
: 한 프로세스의 전체를 cpu가 관리하는 것은 아니다. 중간에 프린터 등 외부 장치가
작업하고 나머지 시간은 쉰다. 

이때 CPU는 대기하고 있던 다른 프로세스를 시작한다.
실제로는 여러 작업들을 돌아가면서 실행하지만, 전체적으로 보면 동시에 하는 것처럼 보인다.
       
* 쓰레드 우선순위
Java에서의 o/s는 JVM 이다. 즉 JVM이 정한 우선순위 스케쥴링 방식을 따른다.


* 쓰레드의 상태
start() 호출했을 때 runnable 상태가 된다.
JVM 스케줄러에 의해 running상태가 된다.
Running( 실행 상태 ) 과 Runnable( 실행 대기 상태 )을 왔다 갔다 하면서 처리된다.  


     

* 쓰레드 메소드
sleep()  - Running 상태의 Thread를 멈추는( blocked )  메소드 // 타이머 역할
join() -  이 메소드를 사용한 Running 중인 Thread가 종료 될 때까지  다른
 쓰레드를 blocked 상태로 만드는 메소드  
// 자원 생산 쓰레드가 끝날 때를, 사용 쓰레드가 기다릴 때 ( 자원 생성 쓰레드.join() )
yield() :  runnalbe 상태 Thread 들 중 우선순위가 같은 Thread가 있으면 실행 중인 Thread 가 Runnalbe 상태가 된다.
우선순위 지정 :  
상수 : MIN_PRIORITY ~   MAX_PRIORITY    // 1 ( ↓ ) ~ 10 ( ↑ )  
기본우선 순위 : 5
setPriority (int 우선순위)
getPriority ( ) : int  
 
