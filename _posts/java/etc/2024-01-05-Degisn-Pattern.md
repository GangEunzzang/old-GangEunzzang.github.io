~~---
title: '[Java] 디자인 패턴 정리'
layout: post
categories: 디자인 패턴
tags: 디자인 패턴
comments: true
---

## 싱글톤 패턴 (SingleTon Pattern)
* 객체를 하나만 만들어 사용하는 패턴
* Socket Connection, DB JDBC Connection, Spring Bean 등 사용

```java
public class Singleton {
    private Singleton(){}

    private static final Singleton singleton = new Singleton();
    
    public static Singleton getInstance() {
        return singleton;
    }
}
```

위와 같이 구현해도 리플렉션으로 private 생성자에 접근 하여 객체 생성시 여러 개의 인스턴스를 생성할 수 있다.   
enum으로 구현하면 완벽한 싱글톤을 보장 받을 수 있으니 구현 방식은 따로 찾아보길 바란다.

## 플라이 웨이트 패턴 (FlyWeight Pattern)
* 인스턴스를 가능한 한 공유해서 사용함으로써 메모리를 절약하는 패턴
* 중복 생성될 가능성이 높거나, 자원 생성 비용은 큰데 사용 빈도가 낮은 경우 적용하면 좋음

```java
public class Flyweight {
    private static Map<String, Subject> map = new HashMap<>();

    public Subject getSubject(Subject subject) {
        String key = subject.name + subject.age;
        if (map.containsKey(key)) {
            return map.get(key);
        }
        
        map.put(key, subject);
        return subject;
    }
}

public class Subject {
    public String name;
    public int age;
    
    public Subject(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```
중복되는 공통된 객체를 생성 할 일이 있다면 자원을 눈에 띄게 아낄수 있을 것이다.

## 빌더 패턴 (Builder Pattern)

기본적으로 멤버 변수가 많아질수록 생성자를 이용하여 생성하기가 힘들어진다.  
순서를 일치시키기도 힘들뿐더러 (물론 ide의 도움이 있긴 하지만 ~ ... 코드를 읽을때 불편함이 있다.)   
기본 생성자로 생성시켜 setter로 일일이 넣어주는 것도 가독성 측면에서 어찌보면 떨어질 수도 있을 것이다.

### 장점
* 가독성/유지보수 향상
* 불변성 확보

```java
class Solution {
    private int a;
    private int b;
    private int c;

    public Solution(int a, int b, int c) {
        this.a = a;
        this.b = b;
        this.c = c;
    }

    public static SolutionBuilder builder() {
        return new SolutionBuilder();
    }
    public static class SolutionBuilder {
        private int a;
        private int b;
        private int c;

        public SolutionBuilder a(int a) {
            this.a = a;
            return this;
        }

        public SolutionBuilder b(int b) {
            this.b = b;
            return this;
        }

        public SolutionBuilder c(int c) {
            this.c = c;
            return this;
        }

        public Solution build() {
            return new Solution(a, b, c);
        }
    }
}
```

사실 대부분 lombok이 지원해주는 @Builder를 사용하여 빌더를 직접 구현할일이 없을것이다.  
하지만 내부 코드가 어떻게 구현이 되는지 이번기회에 한번 접해봤으면 좋겠다 !


## 어댑터 패턴(Adapter Pattern)

* 호출당하는 쪽의 메서드를 호출하는 쪽의 코드에 대응하도록 중간에 변환기(어댑터)를 통해 호출하는 패턴
* 호환성이 없는 기존 클래스의 인터페이스를 변환해서 재사용하기 위해 필요
* 서로 다른 두 인터페이스(클래스) 사이에 통신이 가능하게 하는 것

보통 아래와 같은 구조로 이해하면 된다. (간단한 예시)
```java
public class AdaptorSocket implements Electornic110V {

    private Electornic220V electornic220V;

    public AdaptorSocket(Electornic220V electornic220V) {
        this.electornic220V = electornic220V;
    }

    @Override
    public void powerOn() {
        electornic220V.connect();
    }
}
```   

```java
// APlayer interface
public interface APlayer {
    void play(String fileName);

    void stop();
}

// APlayer 구현체
public class APlayerImpl implements APlayer{

    @Override
    public void play(String fileName) {
        System.out.println("A " + fileName);
    }

    @Override
    public void stop() {

    }
}


// BPlayer interface
public interface BPlayer {
    void playFile(String fileName);

    void stopFile();
}


// BPlayer 구현체
public class BPlayerImpl implements BPlayer{

    @Override
    public void playFile(String fileName) {
        System.out.println("B " + fileName);
    }

    @Override
    public void stopFile() {

    }
}


// 어댑터 BPlayer를 APlayer로
public class BToAAdapter implements APlayer{
    private BPlayer media;

    public BToAAdapter(BPlayer media) {
        this.media = media;
    }

    @Override
    public void play(String fileName) {
        System.out.print("Using Adapter : ");
        media.playFile(fileName);
    }

    @Override
    public void stop() {
    }

    // 변환 가능 ~
    public static void main(String[] args) {
        APlayer player1 = new APlayerImpl();
        player1.play("aaa.mp3");

        BPlayer player2 = new BPlayerImpl();
        player2.playFile("bbb.mp3");

        player1 = new BToAAdapter(new BPlayerImpl());
        player1.play("ccc.mp3");
    }
}

```
위와 같이 adapter를 이용하여 APlayer의 기존 코드 변화없이 다른 객체와 연결시킬 수 있다.


## 참고
