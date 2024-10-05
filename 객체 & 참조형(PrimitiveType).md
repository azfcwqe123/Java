## 참조형

> 참조형 종류 : 배열, 클래스, 인터페이스, 열거형, 제네릭

자바의 메모리 구조에는 메서드 영역, 스택 영역, 힙 영역이 있다. 

참조값은 객체를 저장하는 곳인 힙 영역에 저장된다.

---

객쳬: 클래스의 인스턴스, 메모리에 실제로 존재하는 데이터

참조형: 객체를 가리키는 변수의 타입, 객체의 주소를 저장하는 변수

---

### 배열

```java
package ex2;

public class ArrayMain {
    public static void main(String[] args) {

        // 1. 범위를 미리 정한 케이스
        int[] arr1 = new int[3];


        // 2. 범위를 미리 정하지 않은 케이스
        int[] arr2;
        arr2 = new int[10]; // 범위 설정


        // 3. 원소를 직접 넣어서 결정하는 케이스
        int[] arr3 = {10, 20, 30};
        
    }
}

```

### 클래스

```java
package ex2;

class Person { 

        String name; // 멤버 변수(필드)
        int age; // 멤버 변수(필드)

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

public class PersonMain { // 자바 파일에 public 클래스는 하나만 가능하며, public 클래스 이름이 파일 이름과 같아야 한다.
    public static void main(String[] args) {

        Person person = new Person("Steve", 30); // 객체 생성

        System.out.println("name: " + person.getName());
        System.out.println("age: " + person.getAge());
    }
}

```

```
name: Steve
age: 30
```


### 인터페이스

```java
package ex2;

interface Animal { // 인터페이스 생성
    void sound();
}

class Dog implements Animal { // 인터페이스 상속

    String name;
    int age;

    public Dog(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public void sound() { // Dog 객체는 sound() 메서드를 무조건 구현해야한다.
        System.out.println(getName() + ": Grrrrrrrr");
    }

    public String getName() { // getName() 메서드는 인터페이스의 영향을 받지 않는다.
        return name;
    }

}
public class InterfaceMain {
    public static void main(String[] args) {
        Dog dog = new Dog("A", 5);
        Animal animal = new Dog("B",3); // 다형성, 자동 업캐스팅, 인터페이스를 참조형으로 사용!

        dog.sound();
        animal.sound(); // 오버라이딩 호출해서 Dog 클래스에 있는 sound() 메서드 사용

        // instanceof 연산자를 사용 후, 타입 확인 후 다운캐스팅.
        if(animal instanceof Dog dog1) {
            System.out.println("instancof 사용 다운 캐스팅: " + dog1.getName());
        }

        // 바로 다운캐스팅 후 사용
        ((Dog) animal).sound();
    }
}
 


```

### 열거형

```java

package ex2;

enum Animal { // 열거형 선언
    DOG, CAT, DUCK; // 상수는 대문자로 적는게 관례
}

public class EnumMain {
    public static void main(String[] args) {
        Animal animal = Animal.DOG;

        sound(animal);
    }

    public static void sound(Animal animal) { // 타입 안정성 보장
        switch (animal) {
            case DOG -> System.out.println("왈");
            case CAT -> System.out.println("냐옹");
            case DUCK -> System.out.println("꽉꽉");
        }
    }
}




```

### 제네릭

```java
package ex2;

class Box<T> { // 제네릭 클래스 생성, 타입 매개변수 T
    private T item;

    public void setItem(T item) {
        this.item = item;
    }

    public T getItem() {
        return item;
    }

}

public class GenericMain {
    public static void main(String[] args) {

        // 타입 인자에는 래퍼클래스를 사용해야한다.
        Box<Integer> integerBox = new Box<>(); // 타입 인자 Integer
        integerBox.setItem(100);
        System.out.println(integerBox.getItem());

        Box<String> stringBox = new Box<>(); // 타입 인자 String
        stringBox.setItem("안녕하세요");
        System.out.println(stringBox.getItem());
    }
}

```
제네릭 클래스는 코드 재사용, 타입 안정성을 보장해준다.
