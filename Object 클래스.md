## Object 클래스

1. 최상위 부모 클래스
2. 공통 기본 메서드 제공
3. 다형성

---

Object 클래스는 최상위 부모 클래스로, 모든 자바 클래스는 Object 클래스를 묵시적으로 상속받는다.

```java
public class Person extends Object {  
    
}
```

```java
public class Person { // Object 묵시적 상속.
    
}
```


---

Object 클래스는 Object 클래스에 정의된 메서드(toString(), hashCode(), equals() 등)만 사용 가능.
실제 타입에 다른 객체가 있는 경우, 다운캐스팅해서 해당 객체를 사용할 수 있다.

```java
public class ObjectMain {
    public static void main(String[] args) {

        Dog dog1 = new Dog(); // 참조 타입 : Dog, 실제 타입 : Dog
        Object dog2 = new Dog(); // 참조 타입 : Object, 실제 타입 : Dog
        Object chicken = new Chicken(); // 참조 타입 : Object, 실제 타입 : Chicken
        Object object = new Object(); // 참조 타입 : Object, 실제 타입 : Object

        Object[] arr = {chicken, dog1, dog2, object};

        // ((Dog) object).sound(); // 다운 캐스팅 불가능. 컴파일 오류
        ((Chicken) chicken).sound(); // 다운캐스팅
        System.out.println(object.getClass());
        length(arr);
    }

    static void length(Object[] arr) {
        System.out.println("배열의 길이는: " + arr.length);
    }
}

```
```
꼬끼오
class java.lang.Object
배열의 길이는: 4
```

---

### Object 클래스의 메서드

### equals()
```java
package ex7;

import java.util.Objects;

public class Dog {

    String name;
    int age;

    public Dog(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override // 오버라이딩해서 재정의하는게 일반적. 오버라이딩 하지 않으면 두 객체의 참조값이 같아야 true를 반환하도록 함.
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Dog dog = (Dog) o;
        return age == dog.age && Objects.equals(name, dog.name);
    }
    
}

```

```java
package ex7;

public class ObjectMain {
    public static void main(String[] args) {

        Dog dog1 = new Dog("A",5);
        Dog dog2 = new Dog("B", 10);
        Dog dog3 = new Dog("B", 10);
        
        // fasle
        System.out.println(dog1.equals(dog2));

        // 참조값은 다르지만, 멤버변수가 같으면 true를 반환하도록 equals() 메서드를 오버라이딩해서 재정의함 
        System.out.println(dog2.equals(dog3));

    }
}

```

```java
false
true
```

---

### toString()
```java
package ex7;

public class Dog {

    String name;
    int age;

    public Dog(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override // 오버라이딩해서 toString() 재정의.
    public String toString() {
        return "Dog{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}

```

```java
package ex7;

public class ObjectMain {
    public static void main(String[] args) {

        Dog dog1 = new Dog("A",5);

        System.out.println(dog1); // System.out.println() 메서드는 내부에서 toString()을 호출한다.
    }
}

```

```
Dog{name='A', age=5}
```

toString()을 오버라이딩해서 재정의 하지 않으면, 

toString() 메서드가 객체의 해시 코드를 16진수로 변환한 값을 출력한다. 이 값은 메모리 주소와 관련된 값임.

ex) ex7.Dog@b4c966a

---

### getClass()
```java
package ex7;

public class ObjectMain {
    public static void main(String[] args) {

        Object dog1 = new Dog("A",5); // 다형성
        Object dog2 = new Dog("B", 10); // 다형성
        Object chicken1 = new Chicken("C", 3); // 다형성

        System.out.println(dog1.getClass()); // 객체의 클래스 정보를 출력
        System.out.println(dog2.getClass());
        System.out.println(chicken1.getClass());

        if(dog1.getClass() == dog2.getClass()) {
            System.out.println(true);
        } else {
            System.out.println(false);
        }

        if(dog1.getClass() == chicken1.getClass()) {
            System.out.println(true);
        } else {
            System.out.println(false);
        }

    }
}

```

```
class ex7.Dog
class ex7.Dog
class ex7.Chicken
true
false
```

- getClass()는 컴파일 시점이 아닌 런타임에 객체의 실제 타입에 대한 클래스 정보를 확인하는데 유용함.
- 다형성을 사용할 때, 객체가 어떤 클래스의 인스턴스인지 알아낼 수 있다.

---

### hashCode()
```java
package ex7;

import java.util.Objects;

public class Dog {

    String name;
    int age;

    public Dog(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public int hashCode() { // 오버라이딩해서 재정의하는게 일반
        return Objects.hash(name, age); // 필드를 기반으로 고유한 해시 코드를 생성
    }
}

```

```java
package ex7;

public class ObjectMain {
    public static void main(String[] args) {

        // dog1, dog2는 서로 다른 참조값을 가지고 있다. 하지만 필드는 같다.
        Dog dog1 = new Dog("A", 5); 
        Dog dog2 = new Dog("A", 5);
        Dog dog3 = new Dog("B", 10);

        System.out.println(dog1.hashCode());
        System.out.println(dog2.hashCode());
        System.out.println(dog3.hashCode());

    }
}

```

```
2981
2981
3017
```

- hashCode() 메서드는 객체의 해시 코드를 반환하며, 해시 기반 컬렉션(HashMap, HashSet, HashTable)에서 중요한 역할을 함.
- hashCode() 메서드를 오버라이딩하지 않고 사용하면, 각 객체는 참조값(메모리 주소)를 기반으로 해시 코드가 생성됨. 이때는 필드가 같더라도 참조값이 다르기에 다른 해시코드를 반환함.
