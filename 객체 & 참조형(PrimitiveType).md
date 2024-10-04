## 참조형

> 참조형 종류 : 배열, 클래스, 인터페이스, 열거형, 제네릭

자바의 메모리 구조에는 메서드 영역, 스택 영역, 힙 영역이 있다. 

참조값은 객체를 저장하는 곳인 힙 영역에 저장된다.

---

객쳬: 클래스의 인스턴스, 메모리에 실제로 존재하는 데이터

참조형: 객체를 가리키는 변수의 타입, 객체의 주소를 저장하는 변수

---

### 객체 생성

```java
package ex2;

public class Person {

    String name; // 멤버 변수
    int age; // 멤버 변수

    public Person(String name, int age) { // 생성자
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

}

```

```java
package ex2;

public class PersonMain {
    public static void main(String[] args) {

        Person person = new Person("스티브",30); // 객체 생성

        System.out.println("이름: " + person.getName());
        System.out.println("나이: " + person.age);
    }
}

```
```
이름: 스티브
나이: 30
```

---

### 생성자

