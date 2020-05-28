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
