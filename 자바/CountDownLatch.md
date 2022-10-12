# CountDownLatch  
## CountDownLatch는 어떤 쓰레드가 다른 쓰레드에서 작업이 완료될 때 까지 기다릴 수 있도록 해주는 클래스입니다

* CountDownLatch 작동 원리
CountDownLatch는 다음과 같이 생성할 수 있습니다. 인자로 Latch의 숫자를 전달합니다.

```
CountDownLatch countDownLatch = new CountDownLatch(5); // 카운트다운할 숫자를 작성
countDownLatch.countDown(); // 다음과 같이 countDown()을 호출하면 Latch의 숫자가 1개씩 감소합니다.
countDownLatch.await(); // await()은 Latch의 숫자가 0이 될 때까지 기다리는 코드입니다.
```
다른 쓰레드에서 countDown()을 5번 호출하게 된다면 Latch는 0이 되며, await()은 더 이상 기다리지 않고 다음 코드를 실행하게 됩니다.
그러나 Network,서버 등의 외부에서 어떤 이벤트로 카운트 다운을 못할 경우 
 일정 시간을 초과하면 작업을 기다리지 않도록, **Timeout**을 설정할 수 있습니다.


* 정해진 시간만 기다리기 (Timeout)
``` 
countDownLatch.await(5, TimeUnit.SECONDS); // 5초
```

* 다른 쓰레드 작업이 완료될 때까지 기다리기
``` 
public class CountDownLatchExample {

    public static void main(String args[]) throws InterruptedException {
        CountDownLatch countDownLatch = new CountDownLatch(5);
        List<Thread> workers = Stream
                .generate(() -> new Thread(new Worker(countDownLatch)))
                .limit(5)
                .collect(toList());

        System.out.println("Start multi threads (tid: "
                + Thread.currentThread().getId() + ")");

        workers.forEach(Thread::start);

        System.out.println("Waiting for some work to be finished (tid: "
                + Thread.currentThread().getId() + ")");

        countDownLatch.await();

        System.out.println("Finished (tid: "
                + Thread.currentThread().getId() + ")");
    }

    public static class Worker implements Runnable {
        private CountDownLatch countDownLatch;

        public Worker(CountDownLatch countDownLatch) {
            this.countDownLatch = countDownLatch;
        }

        @Override
        public void run() {
            System.out.println("Do something (tid: " + Thread.currentThread().getId() + ")");
            countDownLatch.countDown();
        }
    }
}
``` 
