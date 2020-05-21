---
layout: post
title: java memory leak,자바 메모리 누수     # Title of the page
author: yunjigo                   
color: rgb(36,41,46)                          # Add the specified color as feature image, and change link colors in post
bootstrap: true                                   # Add bootstrap to the page
tags: [study,java,memory leak,자바 메모리누수]
excerpt_separator: <!--more-->
---

 어디선가 내 메모리를 잡아먹고 있는 것일까  
 자바 메모리 누수에 관련해 알아보자 
 <!--more-->


----
 

### JAVA Memory Leak

![Image Alt](https://www.baeldung.com/wp-content/uploads/2018/11/Memory-_Leak-_In-_Java.png)

우리가 선언하는 객체들은 대부분 Heap memory에 형성되고 이 Heap memory에는 두가지 종류의 객체가 존재한다.  
`참조되는 객체와, 참조되지 않는 객체`이다.  
참조되는 객체는 어플리케이션 내에서 계속 사용되는 객체이고, 참조되지 않는 객체는 더이상 사용하지 않는 객체로 구분한다.  
GC는 참조되지 않는 객체에 대해 실행된다. 하지만, 사용하지는 않는데도 불구하고 참조되는 객체로 분류되는 경우가 있고 이를 memory leak 이라고 한다.  
Old 영역에 누적된 객체로 인해서 메이저 GC가 빈번하게 발생하게 되고, 프로그램의 응답속도가 늦어지다 결국 OOM(OutOfMemory) 오류로 프로그램이 종료되게 된다.  

JAVA 코딩시 대표적으로 나타나는 메모리 누수 유형에 대해 알아보자.

    
      
      

### 1. Autoboxing  
아래의 경우 1000개 가까운 객체가 새롭게 생성되고 Autoboxing되는 작업이 진행된다.  
이러한 primitive 타입과 wrapper 타입간의 Autoboxing을 되도록 피하고 가능한 primitive 타입을 사용하는 것이 좋다.  

```java
public class Adder {
       public long addIncremental(long l)
       {
              Long sum=0L; //wrapper class 형식의 Long으로 선언!
               sum =sum+l; //Autoboxing 으로 인한 메모리 누수!!
               return sum;
       }
       public static void main(String[] args) {
              Adder adder = new Adder();
              for(long i;i<1000;i++)
              {    // 여기서는 primitive 형식의 long으로 넘긴다.
                     adder.addIncremental(i);
              }
       }
}
```

### 2. Using Cache  
아래의 예시는 내부의 Map 데이터 구조 때문에 메모리 누수가 발생한다.  
해당 클래스는 직원들의 정보를 보여주는 cache class이다. 해당 정보는 한번 보여지고 나면,  다른 elements에서는 필요가 없는 정보들이다.  
우리는 해당 cache 정보를 지우는 것을 잊어버리고, cache 정보가 필요없는 모든 객체에 존재한다.  
해당 Map이 GC에서 해당 정보를 지울 수 없도록 강한 연관 관계를 가진다.  

그래서, 아래의 예시처럼 자체의 cache가 필요한 경우에는, 사용후에 clear 해서 해당 데이터들이 더이상 사용되지 않게 명시하거나, WeakHashMap을 사용할 수 있다.  
WeakHashMap은 만약 key들이 다른곳에 참조되지 않으면, GC에 의해 제거되어 발생하는 메모리 누수를 방지할 수 있다.  

```java
import java.util.HashMap;
import java.util.Map;
public class Cache {
       private Map<String,String> map= new HashMap<String,String>();
       public void initCache()
       {
              map.put("윤지", "Work as Java Developer");
              map.put("동진", "Work as Intern");
              map.put("현종", "Work as TeamLeader");
       }
       public Map<String,String> getCache()
       {
              return map;
       }
       public void forEachDisplay()
       {
              for(String key : map.keySet())
              {
                String val = map.get(key);                
                System.out.println(key + " :: "+ val);
              }
       }
       public static void main(String[] args) {       
              Cache cache = new Cache();
              cache.initCache();
              cache.forEachDisplay(); //한번만 사용하고 사용안될건데 계속 유지됨
       }
}
```

    
    
### 3. Using CustomKey  
아래의 CustomKey는  equals() and hashcode() 을 재정의 하지 않았다.   
그래서 저장된  key, value 값은 get 메서드를 실행했을 때 hashcode() 와 equals() 를 사용 할 수 없다.  
그런데도 hashcode() equals()는 GC대상에 포함되지 않는다.  
이미 map에 참조되어 있기 때문인데 아이러니하게도 application에서는 접근을 할 수 없는 것이다.  

이런경우 명확한 메모리 누수가 발생한다. 그래서, Custom key를 만든다면 항상, hashcode() 와 equals()를 구현하는 것이 좋다.  

```java
import java.util.HashMap;
import java.util.Map;
public class CustomKey {
       public CustomKey(String name)
       {
              this.name=name;
       }
       private String name;
       public static void main(String[] args) {
              Map<CustomKey,String> map = new HashMap<CustomKey,String>();
              map.put(new CustomKey("윤지"), "바보");
              String val = map.get(new CustomKey("윤지")); // e
              System.out.println("Missing equals and hascode so value is not accessible from Map " + val);
       }
}

```


### 4. Mutable Custom Key  
아래 코드는 key 정보를 key 정보를 얻은 후 변경할 수 있도록 설계 되어있다.  
이렇게 되면, appplication에서는 해당 정보를 찾을 수 없게되는데 map에서는 계속 참조되고 있기 때문에 메모리 누수가 발생한다.  
이때 key 정보는 바뀌지 않도록 설정해야한다.

```java

import java.util.HashMap;
import java.util.Map;
public class MutableCustomKey {
       public MutableCustomKey(String name)
       {
              this.name=name;
       }
       private String name;
       public String getName() {
              return name;
       }
       public void setName(String name) {
              this.name = name;
       }
       @Override
       public int hashCode() {
              final int prime = 31;
              int result = 1;
              result = prime * result + ((name == null) ? 0 : name.hashCode());
              return result;
       }
       @Override
       public boolean equals(Object obj) {
              if (this == obj)
                     return true;
              if (obj == null)
                     return false;
              if (getClass() != obj.getClass())
                     return false;
              MutableCustomKey other = (MutableCustomKey) obj;
              if (name == null) {
                     if (other.name != null)
                           return  false;
              } elseif (!name.equals(other.name))
                     return false;
              return true;
       }
       public static void main(String[] args) {
              MutableCustomKey key = new MutableCustomKey("윤지");            
              Map<MutableCustomKey,String> map = new HashMap<MutableCustomKey,String>();
              map.put(key, "바보");
              MutableCustomKey refKey = new MutableCustomKey("윤지");
              String val = map.get(refKey);
              System.out.println("Value Found " + val);
              key.setName("동진"); // 키 정보를 바꿔 버림
              String val1 = map.get(refKey); //key 정보가 바뀌어서 가지고 올 수 없지만 계속 참조된 상태로 유지된다.
              System.out.println("Due to MutableKey value not found " + val1);
       }
}
```



### 5. Internal Data Structure 

```java
public class Stack {
       private int maxSize;
       private int[] stackArray;
       private int pointer;
       public Stack(int s) {
              max Size = s;
              stackArray = new int[maxSize];
              pointer = -1;
       }
       public void push(int j) {
              stackArray[++pointer] = j;
       }
       public int pop() {
              return stackArray[pointer--]; // 위치만 전달할 뿐, Stack의 사이즈는 줄어들지 않음. 메모리 누수발생
       }
       public int peek() {
              return stackArray[pointer];
       }
       public boolean isEmpty() {
              return (pointer == -1);
       }
       public boolean isFull() {
              return (pointer == maxSize - 1);
       }
       public static void main(String[] args) {
              Stack stack = new Stack(1000);
              for(int ;i<1000;i++)
              {
                     stack.push(i);
              }
              for(int ;i<1000;i++)
              {
                     int element = stack.pop();
                     System.out.println("Poped element is "+ element);
              }
       }
}
```
위의 코드는 1000의 길이를 가진 stack을 만드는 클래스이다. 각 셀은 값을 설정하지 않아도 해당 메모리를 점유한 상태로 있다. 
보통 pop을 했을 경우 stack의 정보가 사라져야한다. 즉, 정보의 위치 또한 비워져야 한다는 것이다. 하지만, 위의 경우 pop은 해당 위치의 값만 전달해 줄 뿐 사용하지 않는 데이터인지 GC가 판별 할 수가없다. 
그래서 아래와 같이 Array의 사이즈를 수정하여야 한다.

```java
public int pop() {
              int size = pointer--
              int element= stackArray[size];
              stackArray[size];
              return element;
       }
```

### 6. Memory Leak Through static Fields
자바에서 static field의 생명주기는 application의 생명주기와 같다. 
따라서 그만큼 낭비되는 자원도 많을 것이다. 되도록이면, static의 사용은 지양하는 것이 좋다. 
이를 테스트 해보자. 

```java
public class StaticTest {
    //변수를 static으로 생성하고 프로그램을 실행해본다 ---> 이후에 static을 없앤 후 프로그램을 실행해본다.
    //어떤 변화가 생기는지 아래 그림을 통해서 확인하자.
    public static List<Double> list = new ArrayList<>();
  
    public void populateList() {
        for (int i = 0; i < 10000000; i++) {
            list.add(Math.random());
        }
        Log.info("Debug Point 2");
    }
  
    public static void main(String[] args) {
        Log.info("Debug Point 1");
        new StaticTest().populateList();
        Log.info("Debug Point 3");
    }
}
```
이런 프로그램이 실행되는 동안 Heap memory 를 분석해보면, 아래 사진과 같이 points 1과 points2번 사이에 예상했던 대로 heap memory가 증가하게된다. 

![Image Alt](https://www.baeldung.com/wp-content/uploads/2018/11/memory-with-static.png)  

반면 static 을 제거하고 같은 프로그램을 실행하면 

![Image Alt](https://www.baeldung.com/wp-content/uploads/2018/11/memory-without-static.png)

첫번째 구간에서는 거의 같은 변화 양상을 보이지만 시간이 지날수록 populateList() 의 모든 메모리가 GC에 의해  없어진다.  
더이상 참조하지 않기 떄문이다.  
위의 예제를 통해 static 사용을 최소화 해야하는 이유에 대해서 알게 되었다.


줄줄 새는 메모리 누수 이야기 끝~~  
다음에는 메모리 누수 확인하는 툴과 스레드 덤프 관련해서 글을 쓸 예정이다. 

그럼 이만!  

  
![Image Alt bye](/img/bye.gif)


```
  참고 문서   
https://www.baeldung.com/java-memory-leaks
Memory Leaks and Java Code
https://jupiny.com/2019/07/15/java-heap-dump-analysis/
https://stackoverflow.com/questions/26460410/how-can-i-analyze-a-heap-dump-in-intellij-memory-leak
https://stackoverflow.com/questions/42016131/get-error-windbg-erroropendumpfile-failed-when-open-the-core-dump-with-servic
https://d2.naver.com/helloworld/1326256
```
