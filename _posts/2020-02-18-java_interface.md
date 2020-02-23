---
layout: post
title: JAVA - Interface     # Title of the page
author: yunjigo                   
color: rgb(36,41,46)                          # Add the specified color as feature image, and change link colors in post
bootstrap: true                                   # Add bootstrap to the page
tags: [java,interface,study]
excerpt_separator: <!--more-->
---

## Interface <br>
      
자바의 인터페이스는 무엇이고, 언제 어떻게 사용하는 걸까!!
<!--more-->

>인터페이스(interface)는 자바 프로그래밍 언어에서 `클래스들이 구현해야 하는 동작을 지정하는데 사용되는 추상형`이다.    
이들은 프로토콜과 비슷하다. 인터페이스는 interface라는 키워드를 사용하여 선언하며,     
메소드 시그너처와 상수 선언(static과 final이 둘 다 선언되는 변수 선언)만을 포함할 수 있다.     
자바 8 미만의 모든 버전을 기준으로 인터페이스의 모든 메소드는 구현체(메소드 바디)를 포함하고 있지 않다.    
자바 8부터, default와 static 메소드는 interface 정의에 구현체를 가지고 있을 수 있다.    


<br><br><br>

뭔가 백과사전에는 저렇게 나와있는데, 그래서! 어찌 쓰냐궁    
일단 단순한 인터페이스 구조를 보자면 아래와 같다.     
인터페이스 내의 모든 메소드들은 추상메서드이기 때문에 abstract 키워드가 굳이 필요하지 않다.

```java
public interface Predator {
       boolean chasePrey(Prey p);
       void eatPrey(Prey p);
}
```
위의 인터페이스를 구현한 클래스를 보자. 아래와 같다.    

```java
public class Lion implements Predator {

        @Override
        public boolean chasePrey(Prey p) {
               // programming to  chase prey p (specifically for a lion)
        }

        @Override
        public void eatPrey(Prey p) {
               // programming to eat prey p (specifically for a lion)
        }
}
```

### 인터페이스의 상속
인터페이스는 인터페이스를 상속받을수 있다. 아래와 같이 extends로 상속받으며,     
부도 인터페이스에는 없는 기능을 추가로 정의 할 수 있다.
```java
interface 자식인터페이스 extends 부모인터페이스{
}
```
만약, 자식 인터페이스를 구현한 클래스는 **자식 인터페이스와 부모인터페이스의 모두 오버라이딩하여 재 구현해야 한다.**

### 인터페이스의 다중상속

자바의 class는 다중 상속이 허용되지 않는다. 이런 점을 보완하여 interface는 다중 상속이 가능하다.    

```java
interface Parent1{
 void method1();
}

interface Parent2{
 void method2();
} 

//위에 두개의 인터페이스를 구현하는 자바 클래스는 아래와 같다.
//아래와 같이 상속받은 모든 인터페이스의 기능을 구현해야 한다.
public class Child implements Parent1, Parent2{
 @Overrding
 public void method1(){
 }
 
 @Overrding
 public void method2(){
 }
} 
```    
     
---

### 인터페이스의 사용이유

**1.클래스간 결합도를 낮출 수 있다.**
 - 객체지향 설계 원칙의 하나로 클래스간의 영향도는 낮출수로 좋다.(클래스간 간접적인 관계로 변경) 사용자에서 제공자를 직접 사용하지 말고 인터페이스로 사용하면 제공자쪽에 소스의 변경이 있어도 사용자쪽에 직접적인 영향이 없어 변경을 하지 않아도 된다.


**2.표준화가 가능하다.**
 - 클래스이 기본틀을 제공하여 개발자들에게 정형화된 개방을 강요한다.

**3. 서로 무관한 클래스들에게 관계를 맺어준다**
- 하나의 인터페이스를 공통으로 구현하도록 하여 관계를 맺어준다.

**4.개발 시간을 단축 시킬수 있다.**
 - 제공자쪽에서 미 구현되어 있어도 사용자쪽에서 인터페이스 명과 메서드 명만 알고 있어도 사용자쪽에서 개발이 가능하다.

**5.인터페이스를 사용하는 주된 이유는 다형성을 위해서라고 생각한다.**
 - 다형성은 상속받은 클래스 또는 인터페이스의 메서드를 재정의하여 서로 다른 행동을 만들 수 있다.     
상속을 통해 상위 클래스의 타입으로 통일한 후 하위 클래스들을 하나의 타입으로 관리할 수 있다. 이를 사용해서 변경에 유연한 코드를 만들 수 있다.
       
---

### 인터페이스의 이해

인터페이스의 이해를 위해서는 다음 두가지 사항을 숙지하고 있어야 한다.
```
클래스에 대해서 User(사용자)와 Provider(제공자)가 있음
User(사용자)에서는 Provider(제공자) 메서드의 선언부만 알면 됨
```

클래스간의 관계에서 직접적인 관계의 경우 한쪽이 변경되면 다른 한쪽도 변경되어야 하는 단점을 가지고 있다.  
그러나 인터페이스를 매개체로 한 간접적인 관계의 경우 한쪽이 변경되어도 다른 한쪽은 전혀 영향을 받지 않는다.    


<hr/>  

참조하면 좋은 글    
[다형성](https://yunjigo92.github.io/2020/02/22/java_polymorphism.html)



<br><br><br>
이러한 이유들 때문에 자바에서는 인터페이스를 사용한다고 한다.
그럼 이만!!

![Image Alt 텍스트](http://app.jjalbang.today/jj1G9.gif)




>출처    
https://ko.wikipedia.org/wiki/%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4_(%EC%9E%90%EB%B0%94)     
https://sungwoon.tistory.com/59    
https://debugdaldal.tistory.com/171 [달달한 디버깅]    
https://freestrokes.tistory.com/77 [FREESTROKES DEVLOG]    
