---
layout: post
title: thread dump, 스레드 덤프     # Title of the page
author: yunjigo                   
color: rgb(36,41,46)                          # Add the specified color as feature image, and change link colors in post
bootstrap: true                                   # Add bootstrap to the page
tags: [study,java,thread dump,스레드덤프,스레드,자바 스레드]
excerpt_separator: <!--more-->
---

Thread(thread)는 어떠한 프로그램 내에서, 특히 프로세스 내에서 실행되는 흐름의 단위를 말한다.  
일반적으로 한 프로그램은 하나의 Thread를 가지고 있지만, 프로그램 환경에 따라 둘 이상의 Thread를 동시에 실행할 수 있다. 
이러한 실행 방식을 멀티Thread(multithread)라고 한다.

 <!--more-->


----
 

### Thread 와 Process의 차이

![Image Alt thread](https://www.tutorialspoint.com/assets/questions/media/12660/User-level%20threads%20and%20Kernel-level%20threads.PNG)  

멀티프로세스와 멀티Thread는 양쪽 모두 여러 흐름이 동시에 진행된다는 공통점을 가지고 있다. 
하지만 멀티프로세스에서 각 프로세스는 독립적으로 실행되며 각각 별개의 메모리를 차지하고 있는 것과 달리 멀티Thread는 프로세스 내의 메모리를 공유해 사용할 수 있다. 또한 프로세스 간의 전환 속도보다 Thread 간의 전환 속도가 빠르다.  
즉, Thread < 프로세스이며, 하나의 프로세스 내에서 여러개의 Thread가 운영될 수 있다.

### Thread의 종류
#### User-Level Thread
쉽게 말하자면, 우리가 코드로 구현하는 모든 Thread는 User-Level Thread라고 할 수 있다.  
사용자 레벨 Thread는 사용자에 의해 구현되며 커널은 이러한 Thread의 존재를 인식하지 못한다.  
마치 단일 Thread 프로세스인 것처럼 처리한다. 그래서 사용자 레벨 Thread는 커널 레벨 Thread보다 작고 훨씬 빠르다.  
유저 레벨 Thread는 프로그램 카운터 (PC), 스택, 레지스터 및 작은 프로세스 제어 블록으로 사용된다.  
또한 사용자 레벨 Thread 동기화에는 커널이 관여하지 않는다.  
  
  
#### 장점 
사용자 레벨 Thread는 커널 레벨 Thread보다 쉽고 빠르다.  
더 쉽게 관리가 가능하다.  
사용자 레벨 Thread는 모든 운영 체제에서 실행될 수 있다.  
사용자 레벨 Thread에서는 Thread 전환에 필요한 커널모드 권한이 필요없다.  

  
#### 단점 
여러 개의 사용자 Thread 중 하나의 Thread가 시스템 호출 등으로 중단되면 나머지 모든 Thread 역시 중단된다.  
커널이 프로세스 내부의 Thread를 인식하지 못하며 해당 프로세스를 대기 상태로 전환시키기 때문이다.  
시스템 전반에 걸친 스케줄링 우선순위를 지원하지 않는다.(어떤 Thread가 먼저 동작할 지 모른다.)  


#### Kernel-Level Thread
커널 레벨 Thread는 운영 체제에서 직접 처리하며 Thread 관리는 커널에서 수행한다.  
프로세스 및 프로세스 Thread에 대한 컨텍스트 정보는 모두 커널에 의해 관리된다.  
이 때문에 커널 레벨 Thread는 사용자 레벨 Thread보다 느리다.  
하나의 프로세스는 적어도 하나의 커널 Thread를 가지게 된다.  
  
  

#### 장점
커널 레벨 Thread가 차단되더라도 동일한 프로세스 내의 다른 Thread를 커널에서 예약 할 수 있다.  
프로세스의 Thread들을 몇몇 프로세서에 한꺼번에 디스패치 할 수 있기 때문에 멀티프로세서 환경에서 매우 빠르게 동작한다.  
커널이 각 Thread를 개별적으로 관리할 수 있다.  
  
  
#### 단점
프로세스에서 한 Thread에서 다른 Thread로 제어를 전송하려면 모드를 커널 모드로 전환해야해서 느리다. 즉, 사용자 모드에서 커널 모드로의 전환이 빈번하게 이뤄져 성능 저하가 발생한다.  
사용자가 프로그래밍할 때 구현하기 어렵고 자원을 더 많이 소비하는 경향이 있다.  

----


### JAVA에서의 Thread

Thread는 위에서 언급한 것과 같이 다른 Thread와 동시에 실행할 수 있다.  
여러 Thread가 공유 자원을 사용할 때 정합성을 보장하려면 Thread 동기화로 한 번에 하나의 Thread만 공유 자원에 접근할 수 있게 해야 한다. 이를, 자바의 동기화라고 한다.  
Thread 덤프에 대해서 알기 위해서는 먼저, 자바의 Thread에 관해 자세한 이해가 우선되어야 할 기초 지식을 알아보자.  

  
  
#### Monitor란?
Java에서는 Monitor를 이용해 Thread를 동기화한다. 또한기본적으로 Multi Thread 환경을 전제로 설계되었고 동기화 문제를 해결하기 위한 기본적인 메커니즘 제공한다.   
Java에서의 모든 Object는 반드시 하나의 Monitor를 가진다. Object Lock이 Monitor에 해당한다. 특정 Object의 Monitor에는 동시에 하나의 Thread만이 들어갈 수 있다.  
다른 Thread에 의해 이미 점유된 Monitor에 들어가고자 하는 Thread는 Monitor의 Wait Set에서 대기한다. Java에서 Monitor를 점유하는 유일한 방법은 Synchronized 키워드를 사용하는 것인데 Synchronized Statement와 Synchronized Method 두 가지 방법이 있다. Synchronized Statement는 Method내 특정 Code Block에 Synchronized 키워드 사용한 것인데Synchronized Statement를 사용하면 Critical Section에 들어가고 나올 때 Monitor Lock을 수행하는 작업이 Byte Code상에 명시적으로 나타나는 특징이 있다.  
  
  

#### Thread 경합상태(race condition)
기본적으로 경합상태란 둘 이상의 입력 또는 조작의 타이밍이나 순서 등이 결과값에 영향을 줄 수 있는 상태를 말한다.  
입력 변화의 타이밍이나 순서가 예상과 다르게 작동하면 정상적인 결과가 나오지 않게 될 위험이 있는데 이를 경쟁 위험이라고 한다.  
쉽게 설명하자면, 두 개의 Thread가 너도 나도 같은 값을 변경하려고 요청 할 때 경합상태가 발생 한다는 것이다.  
이때 Thread는 다른 Thread가 획득하고 있는 락(lock)이 해제되기를 기다리게 된다.  
웹 애플리케이션에서 여러 Thread가 공유 자원에 접근하는 일은 매우 빈번하다.  
대표적으로 로그를 기록하는 것도 로그를 기록하려는 Thread가 락을 획득하고 공유 자원에 접근하는 것이다.  

  
    
    

#### 교착상태(deadlock)
Thread 경합상태에서 deadlock이 발생하는 경우가 종종있다. 아주 쉽게 설명하자면, 아래 그림과 같다. 이러지도 저러지도 못하는 상태.

![Image Alt thread](https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F270DA73358FC58F207)
  
  
  
  
두 개 이상의 작업이 서로 상대방의 작업이 끝나기 만을 기다리고 있기 때문에 결과적으로 아무것도 완료되지 못하는 상태를 가리킨다.  
예를 들어 하나의 사다리가 있고, 두 명의 사람이 각각 사다리의 위쪽과 아래쪽에 있다고 가정한다.  
이때 아래에 있는 사람은 위로 올라 가려고 하고, 위에 있는 사람은 아래로 내려오려고 한다면, 두 사람은 서로 상대방이 사다리에서 비켜줄 때까지 하염없이 기다리고 있을 것이고
결과적으로 아무도 사다리를 내려오거나 올라가지 못하게 되듯이, 전산학에서 교착 상태란 다중 프로그래밍 환경에서 흔히 발생할 수 있는 문제이다.  
이 문제를 해결하는 일반적인 방법은 아직 없는 상태이다.  

#### 임계 영역(critical section)  
임계 영역 또는 공유변수 영역은 병렬컴퓨팅에서 둘 이상의 Thread가 동시에 접근해서는 안되는 공유 자원(자료 구조 또는 장치)을 접근하는 코드의 일부를 말한다.  
임계 구역은 지정된 시간이 지난 후 종료된다. 때문에 어떤 Thread(태스크 또는 프로세스)가 임계 구역에 들어가고자 한다면 지정된 시간만큼 대기해야 한다.  
Thread가 공유자원의 배타적인 사용을 보장받기 위해서 임계 구역에 들어가거나 나올때는 세마포어 같은 동기화 매커니즘이 사용된다.   


코드예시
```java
do {
      wait(mutex);   //입장 구역
      임계 구역 //이곳이 임계 구역이다!! 하나의 Thread만 접근해야 한다.
      signal(mutex); //퇴장 구역
      나머지 구역
}
```
위에서 본 바와 같이 Thread 경합 때문에 다양한 문제가 발생할 수 있으며, 이런 문제를 분석하기 위해서는 Thread 덤프(Thread Dump)를 이용한다. 각 Thread의 상태를 정확히 알 수 있기 때문이다.  
그렇다면, Thread의 상태는 어떤 것들이 있는지 살펴보자.  


### Thread 상태


![Image Alt thread](/img/tech/thread1.png)  

위의 상태를 그림으로 나타내면 아래와 같다.  

![Image Alt thread](/img/tech/thread2.png)  
  
* NEW: Thread 가 생성되었지만 아직 실행되지 않은 상태  

* RUNNABLE: 현재 CPU 를 점유하고 작업을 수행 중인 상태 . 운영체제의 자원 분배로 인해 WAITING 상태가 될 수도 있다.  

* BLOCKED: Monitor 를 획득하기 위해 다른 Thread 가 Lock 을 해제하기를 기다리는 상태  

* WAITING: wait () Method, join() Method, park() Method 등을 이용해 대기하고 있는 상태  

* TIMED_WAITING: sleep() Method, wait() Method, join() Method, park() Method 등을 이용 해 대기하고 있는 상태.  
  WAITING 상태와의 차이점은 Method 의 인수로 최대 대기 시간을 명시할 수 있어 외부적인 변화뿐만 아니라 시간에 의해서도 WAITING 상태가 해제될 수 있다는 것이다.  
  
  
  
이 상태들에 대한 정확한 이해가 Thread들 간의 Lock 경합을 이해하는데 필수적이다. 만일 특정 Thread가 특정 Object의 Monitor를 장시간 점유하고 있다면
동일한 Monitor를 필요로 하는 다른 모든 Thread들은 BLOCKED 상태에서 대기를 하게 된다. 이 현상이 지나치게 되면 Thread 폭주가 발생하고 자칫 System 장애를 유발할 수 있다.
이런 현상은 Wait Method를 이용해 대기를 하는 경우도 마찬가지이다. 특정 Thread가 장시간 notify를 통해 Wait상태의 Thread들을 깨워주지 않으면 수많은 Thread 들이 WAITING이나 TIMED_WAITING 상태에서 대기를 하게 된다.  
  
### Thread의 종류
#### 데몬 Thread(Daemon Thread)  
 데몬 Thread는 다른 비 데몬 Thread가 없다면 동작을 중지한다. 사용자가 직접 Thread를 생성하지 않더라도 Java 애플리케이션이 기본적으로 여러 개의 Thread를 생성한다.  
 즉, 데몬 Thread는 다른 일반 Thread(비데몬 Thread)의 작업을 돕는 보조적인 역할을 수행하는 Thread이다.  
 일반 Thread가 모두 종료되면 데몬 Thread는 강제적으로 자동 종료되는데, 그 이유는 데몬 Thread는 일반 Thread의 보조 역할을 수행하므로 일반 Thread가 모두 종료되고 나면 데몬 Thread의 존재의 의미가 없기 때문이다.  
 대부분이 데몬 Thread인데 Garbage Collection이나, JMX 등의 작업을 처리하기 위한 것이다.   
   
   

#### 비 데몬 Thread(Non-daemon Thread)
 'static void main(String[] args)' Method가 실행되는 Thread는 비 데몬 Thread로 생성되고, 이 Thread가 동작을 중지하면 다른 데몬 Thread도 같이 동작을 중지하게 되는 것이다.  
 자바에서 비 데몬 Thread는 아래와 같다.  
  * VM Background Thread: Compile, Optimization, Garbage Collection 등 JVM 내부의 일을 수행하는 Background Thread 들이다.
  * Main Thread: main(String[] args) Method 를 실행하는 Thread 로 사용자가 명시적으로 Thread 를 수행하지 않더라도 JVM 은 하나의 Main Thread 를 생성해서 Application 을 구 동한다. Hot Spot JVM 에서는 VM Thread 라는 이름이 부여된다.  
  * User Thread: 사용자에 의해 명시적으로 생성된 Thread 들이다 . java.lang.Thread 를 상속 (extends) 받거나 , java.lang.Runnable 인터페이스를 구현 (implements) 함으로써 User Thread 를 생성할 수 있다.  
  
  
  
------
  
  
### Thread Dump
Java에서 Thread 동기화 문제를 분석하는 가장 기본적인 툴로서 현재 사용 중인 Thread의 상태와 Stack Trace를 출력하고 더불어 JVM의 종류에 따라 더욱 풍부한 정보를 같이 제공한다.  

  
  
#### Thread Dump가 필요한 상황  

모든 시스템에 응답이 없을 때  
사용자 수가 많지 않은데 CPU사용량이 높을때  
특정어플리케이션 수행 시 응답이 없을때  
간헐적으로 응답이 느릴때  
서비스 실행시간이 길어질수록 응답시간이나 cpu 사용량이 늘어날떄 등등  

#### Thread Dump 생성  

반드시 생성시 3~5회 연속으로 생성하여 문제 상황에 대한 변화 과정을 확인해야 한다.  

Unix : kill -3 [PID]  
window : Ctrl + Break  
공통 :  jstack [PID] ( java console에서) 


### Thread Dump 분석
![Image Alt thread](/img/tech/thread3.jpeg)  

##### Thread이름
lang.Thread 클래스로 생성하면 'Thread-숫자' 형식으로 생성된다.  
DefaultThreadFactory 를 사용하면 pool-숫자-thread-숫자 형식으로 생성된다.  
하지만 이런 디폴트이름들로 Thread가 가득하다면 덤프를 읽기가 매우 힘들다. 멀티Thread 프로그래밍을 직접할 경우, setName을 이용해서 직관적인 Thread명을 써주는게 좋다.  

##### 우선순위  
- Thread 우선순위  

##### Thread 아이디  
- 16진수
- tid : 자바레벨 ThreadID, 자바프로세스마다 1부터 시작. 겹칠수 있겠다.
  - ThreadMXBean과 ThreadInfo 을 이용하여 정보 획득 가능  
- nid : 네이티브 ThreadID, OS영역이고 유니크함
  - ps 명령어를 이용해 cpu 사용율 등도 알 수 있음  

##### Thread 상태
- runnable
- blocked
  - deadlock
- wait
##### Thread 콜스택

  
    
    

#### Thread Dump 방법
위에서 Thread dump에 관련한 기본정보를 익혔다면, 실제로 thread dump의 양은 작은 데몬이라고 해도 양이 방대하기 때문에, 분석 사이트를 통해 해결하는 것이 좋다.  
```java
//ThreadMain.java

public static void main(String[] args) {
           ThreadTest atm = new ThreadTest();
           Thread mother = new Thread(atm, "mother");
           Thread son = new Thread(atm, "son");
           mother.start();
           son.start();
       }
``` 

```java
//ThreadTest.java
public class ThreadTest implements Runnable {
 
        private long depositeMoney = 10000;
 
        public void run() {
            synchronized (this) {
                for (int i = 0; i < 10; i++) {
                    notify();
                    try {
                        wait();
                        Thread.sleep(1000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    if (getDepositeMoney() <= 0)
                        break;
                    withDraw(1000);
                }
            }
        }
 
        public void withDraw(long howMuch) {
            if (getDepositeMoney() > 0) {
                depositeMoney -= howMuch;
                System.out.print(Thread.currentThread().getName() + " , ");
            } else {
                System.out.print(Thread.currentThread().getName() + " , ");
                System.out.println("잔액이 부족합니다.");
            }
        }
 
        public long getDepositeMoney() {
            return depositeMoney;
        }
    }
``` 
  
위와같이 간단한 멀티Thread 환경을 구축하고 Thread dump를 떠보았다. intelliJ terminal을 사용했다.  

1. PID 확인  
jps -v 로 현재 사용중인 Thread 데몬들을 확인한다.  
그 중 앞에 보이는 부분이 각 Thread의 PID이다. 그렇다면 확인할 Main Thread의 PID를 확보하고 다음단계로 넘어간다.

![Image Alt thread](/img/tech/thread4.png)  


2. Thread Dump 파일생성.  
jstack -l 22324 > test.txt  
그러면 해당폴더에 text.txt 파일로 해당 Thread에 대한 상세정보가 입력된다.    

3. Thread 상세 확인  
https://fastthread.io/ 사이트로 이동해서, 오른쪽에 있는 곳에 test.txt를 업로드 해본다.  

![Image Alt thread](/img/tech/thread5.png)  


이렇게 내가 생성한  Thread Dump에 대한 상태를 확인할 수 있다. 각각의 상태는 더 상세하게 나오고, Deadlock 이 있는 경우에도 따로 표시되어 나와서,분석하기 용이하게 되어있다. 현재 아래의 Thread의 상태는 WAITING이다.  어떤 부분에서 Thread가 대기상태가 발생했는지 알수 있다.  

![Image Alt thread](/img/tech/thread6.png)  

이렇게 WAIT이 많이 발생하는 경우는 보통 Thread 리소스를 정상적으로 정리하지 못하는 경우
불필요한 Thread가 계속해서 늘어나는 경우이다. Thread 리소스를 정상적으로 정리 못하고 있는 경우이기 각 Thread를 정리하는 모습 혹은 Thread가 종료되는 조건을 확인하는 것이 좋다.  
  



#### Thread Dump로 해결가능한 예제
##### CPU 사용률이 비정상적으로 높을 때 
애플리케이션을 수행할 때 CPU 사용률이 비정상적으로 높다면 Thread 덤프를 이용하여 문제를 파악할 수 있다.  
먼저 다음과 같이 CPU를 가장 많이 점유하는 Thread가 무엇인지 추출한다. (리눅스의 경우  : ps -mo pid,lwp,stime,time,cpu -C java)  
추출한 결과에서 CPU를 가장 많이 사용하는 PID와 NID를 확인한다.  
PID를 16진수로 변환하면 NID를 얻을 수 있다.  
그런다음  PID로  애플리케이션의 Thread 덤프를 생성한 후, 이 Thread 덤프에서 NID가 해당 PID의 16진수인 Thread를 찾아 Thread의 동작을 확인한다.  
Thread 덤프는 시간별로 여러번 떠서 동작하는 동안의 변화를 봐서 분석해야한다.  
  
  
##### 수행 성능이 비정상적으로 느릴 때  
애플리케이션의 수행 성능이 비정상적으로 느릴 때에는 BLOCKED 상태인 Thread가 원인인 경우가 많다.  
이 때에는 Thread 덤프를 여러 번 얻은 다음 BLOCKED 상태인 Thread 목록을 찾고 BLOCKED 상태인 Thread가 획득하려는 락과 관계된 Thread를 추출해 본다.  
Thread의 락을 획득하지 못해 계속 BLCOKED 상태에 있는 경우. 해당 락을 획득하고 있는 Thread의 스택 트레이스(Stack Trace)를 분석하면 문제를 해결할 수 있다.  

##### 실제 사례 
Connection Pool에서 Connection을 얻는 과정에서 Thread 경합이 발생한 것으로 이는 현재 Connection Pool의 완전히 소진되었고  
이로 인해 새로운 DB Request에 대해 새로운 Connection을 맺는 과정에서 성능 저하 현상이 생겼다는 것이다. 

만일 Connection Pool의 최대 Connection 수가 낮게 설정되어 있다면 대기 현상은 더욱 심해질 것이다. 다른 Thread가 DB Request를 끝내고 Connection을 놓을 때까지 기다려야 하기 때문이다.  

해결책은 무엇일까? Connection Pool의 초기 Connection 수와 최대 Connection수를 키운다. 만일 실제 발생하는 DB Request수는 작은데 Connection Pool이 금방 소진된다면 Connection을 닫지 않는 문제일 가능성이 크다.  

이 경우에는 소스 검증이나 모니터링 툴을 통해 Connection을 열고 닫는 로직이 정상적으로 작동하는지 검증해야 한다.  
참고로 다행히 iBatis나 Hibernate같은 프레임 워크들이 보편적으로 사용되면서 JDBC Connection을 잘못 다루는 문제는 거의 없어지고 있다.  


   
   

위과 같이 다양한 서버문제에서 Thread Dump를 통한 해결을 할 수있다.  



  
  
![Image Alt bye](/img/bye.gif)


```
  참고 문서   
데이터산업진흥원 > 정보마당
https://docs.oracle.com/cd/E13150_01/jrockit_jvm/jrockit/geninfo/diagnos/using_threaddumps.html
https://widevery.tistory.com/27 
https://ko.wikipedia.org/wiki/
https://sjh836.tistory.com/151 
https://ijbgo.tistory.com/33 
```
