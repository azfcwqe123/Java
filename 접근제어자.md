### 접근 제어자

|종류|public|default|protected|private|
|:---:|:---:|:---:|:---:|:---:|
|허용 범위|모든 외부 호출|같은 패키지|같은 패키지, 상속관계|모든 외부 호출X, 같은 클래스|

> default는 기본 전제이기 때문에, 명시돼있지 않다.

---

### 같은 패키지 내에서의 코드(package ex1)

```java
package ex1; // 같은 패키지

public class AccessModifier {

    public int a = 100;
    int b = 200; // (default) int b = 200과 같다.
    protected int c = 300;
    private int d = 400;


    public void getA() {
        System.out.println("a 호출 : " + a);
    }

    void getB() { // (default) void getB()와 같다.
        System.out.println("b 호출 : " + b);
    }
    
    protected void getC() {
        System.out.println("c 호출 : " + c);
    }

    private void getD() {
        System.out.println("d 호출 : " + d);
    }

    public void useD() {
        System.out.println("-----------------");
        System.out.println("usdD() 메서드 호출");
        d += 600; // 같은 클래스 내에서는 private 접근이 가능하다.
        getD(); // 이것 또한 마찬가지
    }

}

```

```java
package ex1; // 같은 패키지

public class AccessModifierMain {
    public static void main(String[] args) {

        AccessModifier accessModifier = new AccessModifier();

        accessModifier.getA();
        accessModifier.getB();
        accessModifier.getC();
        // accessModifier.getD(); 컴파일 오류, private 외부 호출 불가능

        accessModifier.useD();
        // 자신의 클래스 내부에서는 private을 호출이 가능하다.
        // 외부 클래스에서는 private에 접근하지 못한다.
        // 이 코드를 호출할 수 있는 이유는, useD() 메서드 자체는 public이기 때문
        
    }
}

```

```
a 호출 : 100
b 호출 : 200
c 호출 : 300
-----------------
usdD() 메서드 호출
d 호출 : 1000
```



> dafault 접근 제어자는 인터페이스의 메서드에만 사용되고, 일반 클래스에서 명시해서 사용하면 컴파일 오류가 발생한다.

> 그렇다면 인터페이스에서 default 접근 제어자를 제외해도 default 접근 제어자는 유효할까?
>
> 정답은 아니다. 인터페이스는 기본적으로 추상 메서드라 <ins>public abstract</ins>가 전제돼있다.

---
### 다른 패키지에서의 코드(package ex1, package ex4)

```java
package ex1; // 다른 패키지

public class AccessModifier {

    public int a = 100;
    int b = 200; // (default) int b = 200과 같다.
    protected int c = 300;
    private int d = 400;


    public void getA() {
        System.out.println("a 호출 : " + a);
    }

    void getB() { // (default) void getB()와 같다.
        System.out.println("b 호출 : " + b);
    }
    
    protected void getC() {
        System.out.println("c 호출 : " + c);
    }

    private void getD() {
        System.out.println("d 호출 : " + d);
    }

    public void useD() {
        System.out.println("-----------------");
        System.out.println("usdD() 메서드 호출");
        d += 600; // 같은 클래스 내에서는 private 접근이 가능하다.
        getD(); // 이것 또한 마찬가지
    }

}

```

```java
package ex4; // 다른 패키지

import ex1.AccessModifier;

class InheritanceClass extends AccessModifier { // 상속 관계

    public void useParentValue() {
        System.out.println("proteced 변수, 메서드 호출");
        getC();
        c += 100;
    }

}

public class InheritanceClassMain {
    public static void main(String[] args) {

        InheritanceClass inheritanceClass = new InheritanceClass();

        inheritanceClass.useParentValue();
    }
}

```

```java
proteced 변수, 메서드 호출
c 호출 : 300
```

---

<ins>클래스 레벨</ins>의 접근 제어자는 public, default만 사용 가능. <ins>생성자</ins>에는 모든 접근 제어자 사용 가능.

```java
class Person {
    
}
```

```java
public class Person {
    
}
```

---

생성자 생성 막는 방법

```java
class Person {

    private Person() {
    } // 생성자 생성 불가능
    
}
```
