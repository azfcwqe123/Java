## 불변 객체

불변 객체는 가변 객체와 달리 한 번 생성하면 객체의 상태(객체 내부의값, 필드, 멤버 변수)를 바꿀 수 없는 객체이다.

객체의 상태가 변하지 않기에 안전성이 보장되고, 캐싱과 재사용에 용이하다.

공유 참조하는 상황일 때, 사이드 이펙트를 방지해주기에 유리하다.

---

#### 불변 객체

```java
package ex9;

public class Person {

    private final int age; // 외부에서 필드 변경 불가
    private final Address address; // 외부에서 필드 변경 불가

    public Person(int age, Address address) {
        this.age = age;
        this.address = address;
    }

    public int getAge() {
        return age;
    }

    public Address getAddress() {
        return address;
    }

    public Person setAddress(Address address) {
        return new Person(this.age, address);
    } // 불변 객체의 값을 바꾸고 싶다면, 새로운 객체를 반환해서 새로 만들면 됨.

    public Person setAge(int age) {
        return new Person(age, this.address);
    } // 불변 객체의 값을 바꾸고 싶다면, 새로운 객체를 반환해서 새로 만들면 됨.


}

```

----

#### 가변 객체

```java
package ex9;

public class Person {

    int age; // 외부에서 필드 변경 가능
    Address address; // 외부에서 필드 변경 가능

    public Person(int age, Address address) {
        this.age = age;
        this.address = address;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public void setAddress(Address address) {
        this.address = address;
    }
}

```

---

#### 불변 객체를 이용한 메서드 체이닝

```java
package ex10;

public class A {

    private final int value;

    public A(int value) {
        this.value = value;
    }

    public A add(int n) {
        return new A(this.value + n);
    }

    public A minus(int n) {
        return new A(this.value - n);
    }

    public int getA() {
        return this.value;
    }
}

```

```java
package ex10;

public class AMain {
    public static void main(String[] args) {
        A a = new A(10);

        A b = a.add(10).add(20).add(30).add(40).minus(10); // 새로운 객체 반환, 버려지는 참조값들은 GC의 대상이 됨

        System.out.println(b.getA());
    }
}

```

```
100
```

객체 a는 여전히 참조되고 있고, 

add(20),add(30),add(40)부분은 새로운 객체가 생성됐다가 GC의 대상이 된다. 

minus(10) 부분은 객체 b가 참조하므로 GC의 대상이 아니게 된다.
