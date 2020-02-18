---
layout: post
title: JAVA - 접근제어자       # Title of the page
author: yunjigo                   
color: rgb(36,41,46)                          # Add the specified color as feature image, and change link colors in post
bootstrap: true                                   # Add bootstrap to the page
tags: [interview,java,study,POJO,spring]
excerpt_separator: <!--more-->
---

## JAVA Access Modifier <br>
      
접근제어자는 멤버 또는 클래스에 사용되어, 해당하는 멤버 또는 클래서를 외부에서 접근하지 못하도록 하는 역할을 한다.
<!--more-->
접근 제어자가 default임을 알리기 위해 실제로 default를 붙이지는 않는다. 클래스나 멤버변수, 메서드<br> 
생성자에 접근제어자가 지정되어 있지 않다면 defalut이다.<br> 
<br> <br> 
그럼 바로 알아보자 😎<br>
접근제어자가 사용될 수 있는 곳 : 클래스, 멤버변수, 메서드, 생성자<br> 

접근제어자의 범위<br> 
<h1> public : 접근 제한이 없다.</h1> 
<h2>protected : 같은 패키지,상속받은 자손클래스라면 다른 패키지에서도 사용가능하다.</h2> 
<h3> default : 같은 패키지 내에서만 사용가능하다.</h3> 
<h4> private : 같은 클래스 내에서만 사용가능하다.</h4>
     
    
----
<br> <br>
       
#### 그렇다면, 접근 제한자는 왜쓰나?
 - 외부로 부터 데이터를 보호하기 위해서
 - 외부에는 불필요한, 내부적으로만 사용되는 부분을 감추기 위해서
(이를 객체지향개념의 캡슐화라고 한다.)
----

#### 제어자의 조합

| 대상 | 사용가능한 제어자 | 
|---|:---:|
| `클래스` | public, (default), final, abstract |
| `메서드` | 모든 접근 제어자, final, abstract, static | 
| `멤버변수` | 모든 접근 제어자, final, static | ( 클래스변수, 인스턴스변수)
| `지역변수` | final |



<br><br><br>

----
#### 더 알면 좋은 제어자 주의사항
##### 1. 메서드에 static과 abstract를 함께 사용할 수 없다.  
static메서드는 몸통이 있는 메서드에만 사용할 수 있기 때문이다.
 
##### 2. 클래스에 abstract와 final을 동시에 사용할 수 없다.    
클래스에 사용되는 final은 클래스를 확장할 수 없다는 의미이고, abstract는 상속을 통해서 완성되어야 한다는 의미이므로 서로 모순된다.

##### 3. abstract메서드의 접근 제어자가 private일 수 없다.    
abstract메서드는 자손클래스에서 구현해주어야 하는데 접근제어자가 private이면, 자손클래스에서 접근할 수 없기 때문이다.

##### 4. 메서드에 private과 final을 같이 사용할 필요가 없다.    
접근제어자가 private인 메서드는 오버라이딩될 수 없기 때문이다. 둘 중 하나만 사용해도 의미가 충분하다.


<br><br><br>
잘 알겠나~~~! 그럼 이만!!

![Image Alt 텍스트](http://app.jjalbang.today/jj1G9.gif)




    출처
    남궁성님의 자바의 정석
    
    
