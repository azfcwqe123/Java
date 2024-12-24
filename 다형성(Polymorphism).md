다형성 : 하나의 객체에 여러가지 타입을 대입할 수 있는 것

```java
package ex01;

public class A { // 부모

    int value = 100;

    public void methodA() {
        System.out.println("A method");
    }

}

```

```java
package ex01;

public class B extends A { // 자식

    int value = 50;

    public void methodB() {
        System.out.println("B method");
    }

}

```

```java
package ex01;

public class lab01 {
    public static void main(String[] args) {
        // new A() -> A 인스턴스가 참조값에 형성됨.
        // 참조값 a는 A 인스턴스를 가르키며, A 인스턴스 사용 가능.
        A a = new A();

        // new B() -> A 인스턴스와 B 인스턴스가 참조값에 형성됨.
        // 참조값 b는 B 인스턴스를 가르키며, A와 B 인스턴스 모두 사용 가능(B는 A를 상속하기 때문).
        B b = new B();

        // new B() -> A 인스턴스와 B 인스턴스가 참조값에 형성됨.
        // 참조값 c는 A 인스턴스를 가르키며, A 인스턴스만 사용 가능
        // B 인스턴스에 있는 값을 사용하려면 다운캐스팅 해야함. 다운캐스팅 할 때는, 메모리에 다운캐스팅 대상이 있는지 꼭 확인해야한다.
        A c = new B();


        a.methodA();
        // a.methodB(); // 부모는 자식 호출 X
        System.out.println();

        b.methodA(); // 자식은 부모 호출 O
        b.methodB();
        System.out.println();

        c.methodA();
        // c.methodB(); // 불가능
        ((B) c).methodB(); // 다운캐스팅. 이건 일시적 다운캐스팅
        System.out.println();

        // 변수는 오버라이딩 되지 않는다. 메서드만 오버라이딩 된다.
        System.out.println("b의 값 : " + b.value);
    }
}

```

결과
```java
A method

A method
B method

A method
B method

b의 값 : 50
```

---

## instanceof

instanceof을 통해 참조값의 인스턴스 타입을 확인 할 수 있다.

```java
package ex01;

public class lab01 {
    public static void main(String[] args) {

        A a = new A();
        B b = new B();
        A c = new B();

        check(a);
        check(b);
        check(c);

    }

    public static void check(A ob) {
        if(ob instanceof B) System.out.println(true);
        else System.out.println(false);
    }

}

```

```java
false
true
true
```

다운 캐스팅을 하기 전에 instanceof을 사용하여 원하는 타입으로 변경이 가능한지 확인하는게 안전하다.
&nbsp;


다운 캐스팅을 하려고 하는데, 참조하려는 인스턴스가 비어있다면 ClassCastException 런타임 에러가 발생하기 때문이다.
&nbsp;

```java
ob instanceof B // 이 부분을 아래와 같이 해석하면 편하다.
new A() instanceof B // 자식 타입은 부모 타입을 담을 수 없다. false
new B() instanceof B // 자신의 타입은 담을 수 있다. true
new B() instanceof B // 자신의 타입은 담을 수 있다. true

// 위에 생성된 객체는 아니지만, C의 부모가 B라고 가정
new C() instanseof B // B는 C의 부모 타입으로써 C을 담을 수 있다. true
```

\-

instanceof으로 타입을 확인 후, 동시에 변수 선언 가능
```java
if(ob instanceof B b) {
    b.methodA();
    b.methodB();
}

// 이렇게 하면 다운캐스팅하는 코드를 생성하지 않아도 됨.
// ex) ((B) ob).methodA();
```

---

