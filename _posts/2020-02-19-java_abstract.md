---
layout: post
title: JAVA - 추상클래스      # Title of the page
author: yunjigo                   
color: rgb(36,41,46)                          # Add the specified color as feature image, and change link colors in post
bootstrap: true                                   # Add bootstrap to the page
tags: [java,interface,study]
excerpt_separator: <!--more-->
---

## 추상클래스란? <br>

추상 클래스(abstract class)란 하나 이상의 추상 메소드(abstract method)를 포함하는 클래스이다. <!--more-->    
추상 메소드는 선언만 있고 본체는 없는 함수이며 선언부에 ‘abstract’ 라는 키워드를 붙인다.     
추상 메소드가 포함되었다면 클래스도 추상 클래스이므로 클래스명 앞에도 ‘abstract’키워드를 붙여야 한다.    


```java
abstract class Dog {
   
    public void move() { …} // 일반 메소드 
    
    //아래와 같이 추상메소드가 하나라도 있으면, 현재 클래스도 추상클래스가 된다.
    abstract void say(); //추상 메소드
}
```

추상 클래스는 추상 메서드를 포함하고 객체화 할 수 없다는 점만 제외하고 일반 클래스와 다르지 않으며     
생성자, 멤버변수와 일반 메서드도 가질 수 있다. 추상 클래스 자체로는 클래스로의 역할을 하지 못하며 객체를 생성할 수 없지만     
새로운 클래스를 작성하는데 있어서 부모 클래스로서 중요한 역할을 갖는다.     
위의 예에서 Dog클래스는 직접 객체를 생성하지 못하고 이를 상속받는 자식 클래스에서는 추상 메소드의 구체적인 본체를 가질 수 있다.    


```java
class MiMi extends Dog {
    public void move() {
        System.out.println("팔짝 팔짝");
    }
    void say() {
            System.out.println("밥줘!!");
    }
}

class BiBi extends Dog { // 추상클래스의 모든 메서드를 구현할 필요는 없다.
    void say() { //추상메소드 구현!!
            System.out.println("산책가자!!");
    }
}

```
위 예에서도 MiMi 클래스는 move()메소드를 오버라이드 했지만 BiBi 클래스는 그러지 않았다.     
하지만 say()메소드는 반드시 구현해야 한다.    
그리고 만약 어떤 추상클래스를 상속 받은 자식 클래스에서 추상 메소드를 구현하지 않았다면     
자식 클래스도 추상 클래스가 되어야 한다는 점도 알아 두자.    


---

<br><br><br>
예제로 우리 강아지들 이름을 썼는데.. 🐶     
말하는 기능을 미미비비가 가졌으면 좋겠다는 생각이 든다.    

그럼 다음 시간에는 인터페이스와 추상클래스의 차이를 알아보자.


![Image Alt 텍스트](http://app.jjalbang.today/jj1G9.gif)




>출처    
https://studymake.tistory.com/423 [스터디메이크]
https://wikidocs.net/219
