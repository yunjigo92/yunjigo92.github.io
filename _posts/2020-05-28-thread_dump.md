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
