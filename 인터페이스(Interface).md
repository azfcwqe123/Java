## 인터페이스 기본

```java
package ex01;

public interface Animal {
    void move(); // 추상 메서드
    void eat(); // 추상 메서드
}

```

```java
package ex01;

public class Chicken implements Animal {
    @Override
    public void move() {
        System.out.println("닭이 움직입니다.");
    }

    @Override
    public void eat() {
        System.out.println("닭이 먹습니다.");
    }
}

```

```java
package ex01;

public class Pig implements Animal {
    @Override
    public void move() {
        System.out.println("돼지가 움직입니다.");
    }

    @Override
    public void eat() {
        System.out.println("돼지가 먹습니다.");
    }
}

```

```java
package ex01;

public class Sheep implements Animal {
    @Override
    public void move() {
        System.out.println("양이 움직입니다.");
    }

    @Override
    public void eat() {
        System.out.println("양이 먹습니다.");
    }
}

```

```java
package ex01;

public class AnimalMain {
    public static void main(String[] args) {

        Animal[] arr = {new Chicken(), new Pig(), new Sheep()};

        for(Animal x : arr) {
            check(x);
            System.out.println("--------------");
        }

    }

    public static void check(Animal animal) {
        animal.eat();
        animal.move();
    }
}

```

```java
닭이 먹습니다.
닭이 움직입니다.
--------------
돼지가 먹습니다.
돼지가 움직입니다.
--------------
양이 먹습니다.
양이 움직입니다.
--------------
```

\- 객체가 인터페이스를 구현할 땐, 해당 객체는 인터페이스의 모든 메서드를 오버라이딩 해야함.

\- 인터페이스가 타입인 변수들은(Animal a) 오버라이딩을 통해서만 자식의 기능을 실행한다. // 메모리 구조 중요함!

\- 인터페이스의 추상 메서드는 public 접근이 기본이다. default 메서드, private 메서드, 정적 메서드도 추가 가능하긴 함.

\- 당연한 것이지만, 추상 메서드를 오버라이딩 하는 자식 메서드는 메서드명, 접근 제어자, 매개변수명까지 모두 똑같이 따라와야 한다.

---

## 인터페이스 다중 구현

```java
package ex01;

public interface Fly {
    void fly();
}

```

```java
package ex01;

public class Chicken implements Animal, Fly {
    @Override
    public void move() {
        System.out.println("닭이 움직입니다.");
    }

    @Override
    public void eat() {
        System.out.println("닭이 먹습니다.");
    }

    @Override
    public void fly() {
        System.out.println("닭이 날고 있습니다.");
    }

}

```

---

## 인터페이스의 상수 필드

```java
package ex02;

public interface Math {
    // = public static final double pi = 3.141592;
    double pi = 3.141592; // 상수 필드
}

```

```java
package ex02;

public class MathMain {
    public static void main(String[] args) {
        System.out.println(Math.pi);
    }
}

```

```
3.141592
```

---

## 인터페이스의 다양한 메서드들

```java
package ex03;

public interface A {

    void methodA();

    default void defaultMethod() {
        System.out.println("defaultMethod() 출력");
    }

    private static void privateMethod() {
        System.out.println("privateMethod() 출력");
    }

    static void staticMethod() {
        System.out.println("staticMethod() 출력");
        privateMethod();
    }

}

```

```java
package ex03;

public class B implements A{

    @Override
    public void methodA() {
        System.out.println("methodA() 출력");
    }

    // defaultMethod()을 재정의 할 때는, public 접근 제어자로 반드시 변경해야됨
    @Override
    public void defaultMethod() {
        System.out.println("defaultMethod() 재정의");
    }


}

```

```java
package ex03;

public class Main {
    public static void main(String[] args) {
        A.staticMethod(); // 인터페이스의 정적 메서드는 구현 객체 없이 접근 가능

        A b = new B();

        b.defaultMethod();
        b.methodA();
    }
}

```

```
staticMethod() 출력
privateMethod() 출력
defaultMethod() 재정의
methodA() 출력
```

---

## 인터페이스 상속(O), 구현(X)

인터페이스는 클래스와 다르게 다중 상속이 가능함.
```java
public interface A {
    void methodA();
}

```

```java
public interface B {
    void methodB();
}
```

```java
public interface C extends A, B{
    void methodC();
}
```

```java
public class Son implements C{

    @Override
    public void methodA() {
        System.out.println("methodA() 실행");
    }

    @Override
    public void methodB() {
        System.out.println("methodB() 실행");
    }

    @Override
    public void methodC() {
        System.out.println("methodC() 실행");
    }
}
```

```java
class Main {
    public static void main(String[] args) {

        A a = new Son();
        a.methodA();
        System.out.println("-----------");
        B b = new Son();
        b.methodB();
        System.out.println("-----------");
        C c = new Son();
        c.methodA();
        c.methodB();
        c.methodC();

    }
}
```

```
methodA() 실행
-----------
methodB() 실행
-----------
methodA() 실행
methodB() 실행
methodC() 실행
```

---
