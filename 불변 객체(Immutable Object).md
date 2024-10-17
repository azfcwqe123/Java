## 불변 객체

불변 객체는 가변 객체와 달리 한 번 생성하면 필드의 값을 바꿀 수 없는 객체이다.

객체의 상태가 변하지 않기에 안전성이 보장되고, 사이드 이펙트를 방지해주며 캐싱과 재사용에 용이하다.

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
