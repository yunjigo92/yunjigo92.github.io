---
layout: post
title: JAVA - 다형성(polymorphism)      # Title of the page
author: yunjigo                   
color: rgb(36,41,46)                          # Add the specified color as feature image, and change link colors in post
bootstrap: true                                   # Add bootstrap to the page
tags: [java,다형성,study]
excerpt_separator: <!--more-->
---

## 다형성 <br>
      
다형성이란 무엇인지 알아보자. 그리고, 자바에서는 다형성을 어떻게 사용할까?
<!--more-->
      
그의 사전적 정의는 아래와 같다.

>프로그램 언어의 다형성(多形性, polymorphism; 폴리모피즘)은 그 프로그래밍 언어의 자료형 체계의 성질을 나타내는 것으로,     
프로그램 언어의 각 요소들(상수, 변수, 식, 오브젝트, 함수, 메소드 등)이 다양한 자료형(type)에 속하는 것이 허가되는 성질을 가리킨다.    
반댓말은 단형성(monomorphism)으로, 프로그램 언어의 각 요소가 한가지 형태만 가지는 성질을 가리킨다.     


<br><br><br>


<hr/>  


다형성은 상속과 깊은 관계가 있다.    

객체지향개념에서 다형성이란 '여러 가지 형태를 가질 수 있는 능력'을 의미하며     
자바에서는 한 타입의 참조변수로 여러 타입의 객체를 참조할 수 있도록함으로써 다형성을 프로그램적으로 구현하였다.    
이를 좀 더 구체적으로 말하자면, 조상클래스 타입의 참조변수로 자손클래스의 인스턴스를 참조할 수 있도록 하였다는 것이다.

```java
class Car {/*구현*/}

class FireEngine extends Car {/*구현*/}

public static void main(String[] args) {

    /*자기 자신을 참조하여 객체 생성*/
    Car c = new Car();

    /*자기 자신보다 범위가 넓은 자식클래스를 참조하여 객체 생성*/
    // 자식클래스를 참조하고 있지만 Car의 인스터스 이므로 Car에 정의된 멤버만 사용가능!!!
    Car c1 = new FireEngine();
    
    /*형변환 하여 객체 생성*/
    // Car를 참조했지만 형변환을 했으므로 Car의 메소드를 포함혀어 FireEngin의 모든 기능 사용가능!!
    // 참고로 이 경우는 형변환 하지 않으면 에러가 난다.
    FireEngin f = (FireEngine)new Car();
}
```
참고로 c는 Car의 인스턴스이고 c1은 Car의 인스턴스이자 FireEngine의 인스턴스이다.     

```java
//아래의 InterfaceTestClass는 상속받은 모든 인터페이스의 기능들이 구현되어 있을것이다.
public class InterfaceTestClass implements InterfaceTest1 , InterfaceTest2, InterfaceTest3{/*구현*/}


//하지만 아래처럼 사용한다면!!
public static void main(String[] args) {
    InterfaceTest1 i1 = new InterfaceTestClass(); // InterfaceTest1 기능만 사용가능
    InterfaceTest2 i2 = new InterfaceTestClass(); // InterfaceTest2 기능만 사용가능
    InterfaceTest3 i3 = new InterfaceTestClass(); // InterfaceTest3 기능만 사용가능
}
``` 
Java에서 다형성은 상속과 인터페이스를 통해 이루어진다.     
인터페이스는 클래스의 선언 뒤에서 여러 개의 인터페이스를 구현할 수 있게 할 수 있다.    
이런 이유 때문에 하나의 객체를 여러 개의 타입으로 바라보는 다형성에는 상속보다 인터페이스가 더 큰 유연함을 제공한다.




<br><br><br>

![Image Alt 텍스트](http://app.jjalbang.today/jj1G9.gif)




>출처    
https://ko.wikipedia.org/wiki/%EB%8B%A4%ED%98%95%EC%84%B1_(%EC%BB%B4%ED%93%A8%ED%84%B0_%EA%B3%BC%ED%95%99)
자바의 정석
