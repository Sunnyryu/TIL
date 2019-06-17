# 자바 기초 복습9

## First. 쓰레드, I/O 외 정리

- 데이터 표현

  - 날짜 데이터처리 및 날짜 데이터 표현
    - java.util.Data d = new Data();
    - d = new Date(long millisecond)
  - java.util.Calendar cal = Calendar.getInstance();
  - 현재 월  -> cal.get(Calendar.MONTH)
  - 5.31일로 설정하기 위해서는 => cal.set(2019, 4, 31)
  - 6월 1일로 만들려면 cal.add(Calender.DATE.1)
  - 날짜 데이터를 특정 형식으로 문자열화하려면 : yyyy-MM-dd hh:mm:ss
    - java.text.simpleDateFormat 클래스를 사용해야함.
    - SimpleDateFormat 클래스를 사용해야함.
    - Date d = new Date();
    - sdf.format(d);
  - 숫자 데이터를 특정 형식으로 문자열화하려면
    - java.text.DecimalFormat, double won = 12345.678
    - DecimalFormat df = new DecimalFormat("\u00A4##,###.");
    - String s = df.format(won);
  - 특정 형식으로 문자열화된 데이터를 숫자로 변환하려면
    - df.parse(s)

- 입출력

  - 표준 출력 = 콘솔 출력!
  - Stream - 흐름
  - 특성 : FIFO
  - 소스에서 데이터,스트림를 타겟으로 보내고 타겟은 스트림을 읽음 -  큐 구조임(소스에서는 매우 빠르지만 타겟은 느리다보니 처리가 늦고 지연이 됌)
  - 단방향으로 갔다리 왔다리 함!! 소스 - > 타겟( 소스 입장에서는 쓰기 스트림 하나 생성) / 타겟 - > 소스 (소스 입장에서는 읽기 스트림 하나 생성) 
    - XXXInputStream, XXXOutputStream - 1byte
    - CharecterStream은 XXXReader나 XXXWriter로 끝남. - 2byte
    - 1차 스트림 - 직접 read나 write하는 것을 쓸 수 있음
    - 2차 스트림 - 변환을 해서 사용함, buffer를 이용해서 처리단위를 buffer에 들어가있는 만큼으로 바꿔서 성능을 개선함, 
    - 필터 처리를 하여 걸러내어 사용할 수 있음!

  ```java
  // System.in으로 체이닝 해서 사용함 1.2차 스트링 예시 
  // InputStream is = new InputStream(); X
  // InputStream is = System.in; 
  // (추상 클래스)
  // OutStream os = new OutputStream(); X
  // OutStream os = new File OutputStream(); O
  // OutStream os = System.out; //PrintStream 
  ```

  - 파일은 스트림이 아님, 추상화한 것이고 내용 변경 불가
    - 메타정보 확인 가능 , length는 얼마고 그러한 것을 확인 가능

- 쓰레드

  - 동작하고 있는 프로그램을 프로세스(Process)라고 한다. 
  - 보통 한 개의 프로세스는 한 가지의 일을 하지만, 
  - 이 쓰레드를 이용하면 한 프로세스 내에서 두 가지 또는 그 이상의 일을 동시에 가능.

```java
public class Test extends Thread {
    public void run() {
        System.out.println("thread run.");
    }

    public static void main(String[] args) {
        Test test = new Test();
        test.start();
    }
```

```java
public class Test extends Thread {
    int seq;
    public Test(int seq) {
        this.seq = seq;
    }
    public void run() {
        System.out.println(this.seq+" thread start.");
        try {
            Thread.sleep(1000);
        }catch(Exception e) {

        }
        System.out.println(this.seq+" thread end.");
    }

    public static void main(String[] args) {
        for(int i=0; i<10; i++) {
            Thread t = new Test(i);
            t.start();
        }
        System.out.println("main end.");
    }
}
//총 10개의 쓰레드를 실행시키는 예제이다. 어떤 쓰레드인지 확인하기 위해서 쓰레드마다 생성자에 순번을 부여했다. 그리고 쓰레드 메소드(run) 수행 시 시작과 종료를 출력하게 했고 시작과 종료 사이에 1초의 간격이 생기도록(Thread.sleep(1000)) 작성했다.

//그리고 main 메소드 종료 시 "main end."를 출력하도록 했다.

//결과는 다음과 비슷하게 나올 것이다.
```

- 예를 통한 나머지 개념 이해

```java
//ex 1)
public static void main(String[] args) {
    ArrayList<Thread> threads = new ArrayList<Thread>();
    for(int i=0; i<10; i++) {
        Thread t = new Test(i);
        t.start();
        threads.add(t);
    }

    for(int i=0; i<threads.size(); i++) {
        Thread t = threads.get(i);
        try {
            t.join(); // join 메소드는 쓰레드가 종료될 때까지 기다리게 하는 메서드
        }catch(Exception e) {
        }
    }
    System.out.println("main end.");
   //ex 2)
    import java.util.ArrayList;

public class Test implements Runnable {// run 메소드를 시작하게 해줌.
    int seq;
    public Test(int seq) {
        this.seq = seq;
    }
    public void run() {
        System.out.println(this.seq+" thread start.");
        try {
            Thread.sleep(1000);
        }catch(Exception e) {
        }
        System.out.println(this.seq+" thread end.");
    }

    public static void main(String[] args) {
        ArrayList<Thread> threads = new ArrayList<Thread>();
        for(int i=0; i<10; i++) {
            Thread t = new Thread(new Test(i));
            t.start();
            threads.add(t);
        }

        for(int i=0; i<threads.size(); i++) {
            Thread t = threads.get(i);
            try {
                t.join();
            }catch(Exception e) {
            }
        }
        System.out.println("main end.");
    }
```

- 그외 용어
  - 데몬 쓰레드 :우선순위가 낮은 쓰레드를 만들어서 보조역할을 함..
    (일반 쓰레드가 끝나면 ... 존재의 의미가 없음)
  - 쓰레드는 모두가 균등하게 쓰길 원함
  - not exist -(new Thread)- new- (start호출, 스레드 스케쥴러호출) - Ready (Run) - Runnable (run메소드 시작) - 스레드가 죽음 (다시 시작못함, 죽으면 새로 쓰레드르 생성해야함
  - 마지막 쓰레드는 어플리케이션이 종료되면 종료됨, 프로그램을 종료시켜야 할 때 종료가 안되어있다면, 데몬 쓰레드를 이용해 종료시키면 좋음