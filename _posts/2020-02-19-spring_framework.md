---
layout: post
title: Spring Framework 정리     # Title of the page
author: yunjigo                   
color: rgb(36,41,46)                          # Add the specified color as feature image, and change link colors in post
bootstrap: true                                   # Add bootstrap to the page
tags: [java,spring,framework,DI,study,AOP,IoC]
excerpt_separator: <!--more-->
---

## Spring Framwork <br>
      
 스프링 프레임 워크, 낱낱히 파헤쳐보자.😎
<!--more-->

![Image Alt 텍스트](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Spring_Framework_Logo_2018.svg/200px-Spring_Framework_Logo_2018.svg.png)

스프링 프레임워크(영어: Spring Framework)는 자바 플랫폼을 위한 오픈 소스 애플리케이션 프레임워크로서 간단히 스프링(Spring)이라고도 한다.     
동적인 웹 사이트를 개발하기 위한 여러 가지 서비스를 제공하고 있다.      
대한민국 공공기관의 웹 서비스 개발 시 사용을 권장하고 있는 전자정부 표준프레임워크의 기반 기술로서 쓰이고 있다.     
(실제로 우리팀도 현재 금융플랫폼 개발을 전자정부 프레임워크로 사용하고 있다.)

---

### 스프링의 주요특징

- 경량 컨테이너로서 자바 객체를 직접 관리한다. 각각의 객체 생성, 소멸과 같은 라이프 사이클을 관리하며스프링으로부터 필요한 객체를 얻어올 수 있다.    
- 스프링은 Plain Old Java Object 방식의 프레임워크이다.( POJO에 대해서는 지난 포스트를 참고하기 바란다!!!)     
일반적인 J2EE 프레임워크에 비해 구현을 위해 특정한 인터페이스를 구현하거나 상속을 받을 필요가 없어 기존에 존재하는    
라이브러리 등을 지원하기에 용이하고 객체가 가볍다.
- 스프링은 `제어 반전(IoC : Inversion of Control)`을 지원한다. 컨트롤의 제어권이 사용자가 아니라 프레임워크에 있어서 필요에 따라 스프링에서 사용자의 코드를 호출한다.    
- 스프링은 `의존성 주입(DI : Dependency Injection)`을 지원한다. 각각의 계층이나 서비스들 간에 의존성이 존재할 경우 프레임워크가 서로 연결시켜준다.    
- 스프링은 `관점 지향 프로그래밍(AOP : Aspect-Oriented Programming)`을 지원한다. 따라서 트랜잭션이나 로깅, 보안과 같이 여러 모듈에서 공통적으로 사용하는 기능의 경우 해당 기능을 분리하여 관리할 수 있다.    
- 스프링은 `영속성과 관련된 다양한 서비스를 지원한다.` iBATIS나 하이버네이트 등 이미 완성도가 높은 데이터베이스 처리 라이브러리와 연결할 수 있는 인터페이스를 제공한다.    
- 스프링은 확장성이 높다. 스프링 프레임워크에 통합하기 위해 간단하게 `기존 라이브러리를 감싸는 정도로 스프링에서 사용이 가능하기 때문에` 수많은 라이브러리가 이미 스프링에서 지원되고 있고 스프링에서 사용되는 라이브러리를 별도로 분리하기도 용이하다.    

---

### 주요 모듈

**제어 반전 컨테이너**
제어 반전(IoC: Inversion of Control) 컨테이너는 스프링의 가장 중요하고 핵심적인 기능으로서 `자바의 반영(reflection)을 이용해서 객체의 생명주기를 관리하고 의존성 주입(Dependency Injection)을 통해 각 계층이나 서비스들간의 의존성을 맞춰준다.` 이러한 기능들은 주로 환경설정을 담당하는 XML 파일에 의해 설정되고 수행된다.
<br><br>
**관점 지향 프로그래밍 프레임워크**
스프링은 로깅이나 보안, 트랜잭션 등 핵심적인 `비즈니스 로직과 관련이 없으나 여러 곳에서 공통적으로 쓰이는 기능들을 분리하여 개발하고 실행 시에 서로 조합할 수 있는 관점 지향 프로그래밍(AOP)을 지원한다`. 기존에 널리 사용되고 있는 강력한 관점 지향 프로그래밍 프레임워크인 AspectJ도 내부적으로 사용할 수 있으며, 스프링 자체적으로 지원하는 실행시(Runtime)에 조합하는 방식도 지원한다.
<br><br>
**데이터 액세스 프레임워크**
스프링은 데이터베이스에 접속하고 자료를 저장 및 읽어오기 위한 여러 가지 유명한 라이브러리, `즉 JDBC, iBATIS(MyBatis), 하이버네이트 등에 대한 지원 기능을 제공하여 데이터베이스 프로그래밍을 쉽게 사용`할 수 있다.
<br><br>
**트랜잭션 관리 프레임워크**
스프링은 추상화된 트랜잭션 관리를 지원하며 XML 설정파일 등을 이용한 선언적인 방식 및 프로그래밍을 통한 방식을 모두 지원한다.
<br><br>
**모델-뷰-컨트롤러 패턴**
스프링은 웹 프로그램밍 개발 시 거의 표준적인 방식인 Spring MVC라 불리는 모델-뷰-컨트롤러(MVC) 패턴을 사용한다. `DispatcherServlet이 Controller 역할을 담당하여` 각종 요청을 적절한 서비스에 분산시켜주며 이를 각 서비스들이 처리를 하여 결과를 생성하고 그 결과는 다양한 형식의 View 서비스들로 화면에 표시될 수 있다.
<br><br>
**배치 프레임워크**
스프링은 특정 시간대에 실행하거나 대용량의 자료를 처리하는데 쓰이는 일괄 처리(Batch Processing)을 지원하는 배치 프레임워크를 제공한다. 기본적으로 `스프링 배치는 Quartz 기반으로 동작`한다.

<br><br>

---
뭐 구구절절 장점도 많고, 모듈도 많이 사용하는 건 알겠다.   
그럼 대체 제어의 역전은 뭐고 의존성 주입은 또 뭘까낭..?   
더 깊이 알아보자!! 😎👌   

### IoC란?
전통적인 프로그래밍에서 흐름은 프로그래머가 작성한 프로그램이 외부 라이브러리의 코드를 호출해 이용한다.    
하지만 제어 반전이 적용된 구조에서는` 외부 라이브러리의 코드가 프로그래머가 작성한 코드를 호출한다.`    
설계 목적상 제어 반전의 목적은 다음과 같다.    
- 작업을 구현하는 방식과 작업 수행 자체를 분리한다.    
- 모듈을 제작할 때, 모듈과 외부 프로그램의 결합에 대해 고민할 필요 없이 모듈의 목적에 집중할 수 있다.    
- 다른 시스템이 어떻게 동작할지에 대해 고민할 필요 없이, 미리 정해진 협약대로만 동작하게 하면 된다.    
다음의 예를 보자

```java
public class Yunji{
  public Object say(Object obj){
  
    if(businessLayer.check(obj){  // businessLayer에서 값을 확인하는 작업과
      DAO.getData(obj);
      return Aspect.convertData(obj); // 데이터를 변환하는 작업이 이미 정해져있다.
    }
    return null;
  }
}
// 이런 방식으로 사용하면, Yunji 객체는 Dao와 완전히 결합하게 되어, 유연한 코드를 작성할 수 없다.
// 아래의 방식을 보자.
public class Yunji{
  public Object say(Object obj, DAO dao){ // 이런식으로 구현하게 되면, dao에 제어권을 넘기게 된다.
    return dao.getData(obj);
  }
}
```
그럼 스프링프레임 워크는 어떻게 IoC를 구현 하는걸까?  
바로. DI 디자인 패턴을 통하여 구현하게 된다.

---

### DI란?
의존성 주입(Dependency Injection, DI)은 프로그래밍에서 `구성요소간의 의존 관계가 소스코드 내부가 아닌 외부의 설정파일 등을 통해 정의되게 하는 디자인 패턴` 중의 하나이다.    
#### DI의 장접
- 의존 관계 설정이 컴파일시가 아닌 실행시에 이루어져 모듈들간의 결합도 를 낮출 수 있다.    
- 코드 재사용을 높여서 작성된 모듈을 여러 곳에서 소스코드의 수정 없이 사용할 수 있다.    
- 모의 객체 등을 이용한 단위 테스트의 편의성을 높여준다.    

#### 주입방식
- 생성자 주입 : 필요한 의존성을 모두 포함하는 클래스의 생성자를 만들고 그 생성자를 통해 의존성을 주입한다.    
- 세터(Setter)를 통한 주입 : 의존성을 입력받는 세터(Setter) 메소드를 만들고 이를 통해 의존성을 주입한다.    
- 인터페이스(Interface)를 통한 주입 : 의존성을 주입하는 함수를 포함한 인터페이스를 작성하고 이 인터페이스를 구현하도록 함으로써 실행시에 이를 통하여 의존성을 주입한다.    

---

### AOP란?

컴퓨팅에서 관점 지향 프로그래밍(aspect-oriented programming, AOP)은 `횡단 관심사(cross-cutting concern)의 분리`를 허용함으로써 모듈성을 증가시키는 것이 목적인 프로그래밍 패러다임이다. 코드 그 자체를 수정하지 않는 대신 기존의 코드에 추가 동작(어드바이스)을 추가함으로써 수행하며, `"함수의 이름이 'set'으로 시작하면 모든 함수 호출을 기록한다"와 같이 어느 코드가 포인트컷(pointcut)` 사양을 통해 수정되는지를 따로 지정한다. 이를 통해 기능의 `코드 핵심부를 어수선하게 채우지 않고도 비즈니스 로직에 핵심적이지 않은 동작들을 프로그램에 추가`할 수 있게 한다. 관점 지향 프로그래밍은 관점 지향 소프트웨어 개발의 토대를 형성한다.

#### 횡단 관심사의 성격을 가진 예를 보자.
동기화   
실시간 제약조건   
오류 검출 정정   
제품 기능   
메모리 관리   
자료 검증    
트랜잭션 처리   
국제화와 지역화 (언어 현지화 포함)
정보 보안   
캐시 처리    
로깅   

로깅을 생각하면 쉽다. 고객이 어떤 메소드를 호출할 때마다 생성되야 하는 것이 로그다.    
이런 것을 코드와 분리하여 사용하면 조금 더 효율적인 방식으로 코드를 작성할 수 있고, 유지보수에도 좋다!!   
직접 코드로 확인해보자.    
```java
void tranfer(Account fromAcc, Account toAcc, int amount, User user,Logger logger, Database database) throws Exception {
  //로그를 찍는다.
  logger.info("돈을 바꿔 바꿔~~~~~~바꾸는중이야~~~");

   //비지니스 로직 가득가득 담겨있어 
  if (!isUserAuthorised(user, fromAcc)) {
    logger.info("User has no permission.");
    throw new UnauthorisedUserException();
  }
      ...... (많은 로직)....

   //로그를 또 찍는다.
  logger.info("Transaction successful.");
 }

//위와 같이 구현하게되면 모든 기능에 해당 로그를 찍는 코드를 생성해야한다.
//이를 위해 아래처럼 바꾸어 사용하자.

aspect Logger {
  void Bank.transfer(Account fromAcc, Account toAcc, int amount, User user, Logger logger)  {
    logger.info("돈을 바꿔 바꿔~~~~~~바꾸는중이야~~~");
  }
  //이와 같이하면, 해당 메소드가 호출될때마다 로그가 찍힌다. 깔-끔하고 유지보수도 간단한 것을 알 수 있다.
}
```

<br><br>


### 스프링프레임 워크의 기본동작

```
Request -> DispatcherServlet -> HandlerMapping -> Controller -> Service -> DAO -> DB    
-> DAO -> Service -> Controller -> DispatcherServlet -> ViewResolver -> View -> Response
```


이 밖에도 스프링에 대해서는 공부할게 많지만, 다음장에서 다루기로 하고
그럼 이만!!

![Image Alt 텍스트](http://app.jjalbang.today/jj1G9.gif)



>출처    
https://ko.wikipedia.org/wiki/%EC%A0%9C%EC%96%B4_%EB%B0%98%EC%A0%84
https://ko.wikipedia.org/wiki/%EC%8A%A4%ED%94%84%EB%A7%81_%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC
https://intro0517.tistory.com/151    
토비의 스프링


