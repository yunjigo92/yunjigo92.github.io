---
layout: post
title: JAVA - Interface       # Title of the page
author: yunjigo                   
color: rgb(36,41,46)                          # Add the specified color as feature image, and change link colors in post
bootstrap: true                                   # Add bootstrap to the page
tags: [java,interface,study]
excerpt_separator: <!--more-->
---

## Interface  <br>
      
자바의 인터페이스는 무엇이고, 언제 어떻게 사용하는 걸까!!
<!--more-->

>인터페이스(interface)는 자바 프로그래밍 언어에서 ***클래스들이 구현해야 하는 동작을 지정하는데 사용되는 추상형***이다.    
이들은 프로토콜과 비슷하다. 인터페이스는 interface라는 키워드를 사용하여 선언하며,     
메소드 시그너처와 상수 선언(static과 final이 둘 다 선언되는 변수 선언)만을 포함할 수 있다.     
자바 8 미만의 모든 버전을 기준으로 인터페이스의 모든 메소드는 구현체(메소드 바디)를 포함하고 있지 않다.    
자바 8부터, default와 static 메소드는 interface 정의에 구현체를 가지고 있을 수 있다.    



---


---

#### 1. 지역변수   
메소드 내에 선언되며 메소드 호출시 생성되고 메소드가 종료되면 사라진다.    
    
#### 2.매개변수    

흔히 파라미터라고 불린다. 메소드에서 입력값을 받을 때가 있는데 그때 사용되는 변수를 매개변수라고 한다.
매개변수도 매소드 내에 선언된 것으로 간주되므로 지역변수이다.
인자값은 호출시 메소드입력부의 넣는 값이며 이값은 매개변수에 복사되어 대입된다.    


---
코드로 간단히 보면 아래와 같다.


```java
public class test { 
    int iv; // 인스턴스 변수 
    static int cv; // 클래스 변수 
    
    void method(int a //매개변수) { 
        int lv; // 지역 변수
    } 
}

```

<br>


-----


<br><br><br>
변수안뇽 그럼 이만!!

![Image Alt 텍스트](http://app.jjalbang.today/jj1G9.gif)




>출처    
https://sleepyeyes.tistory.com/28    
https://itmining.tistory.com/20
    
    
    
