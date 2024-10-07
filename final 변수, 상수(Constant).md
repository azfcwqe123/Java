## fianl 변수

1. fianl 변수는 한 번 초기화하면 끝난다.

2. final 키워드는 프로그램의 안전성과 유지보수성을 높이는 데 중요함.

---

### final 변수에 선언

```java
final int a = 10;
//a = 20; 컴파일 에러
```
---

### 멤버 변수에 선언

```java
class Person {
    final String name = "Steve"; // 인스턴스 생성과 동시에 할당되며, 변경 불가능
}
```

---


### 생성자에 선언

```java
class Person {
    final String name;

    public Person(String name) {
        this.name = name;
    }
}
```

---

### 참조형 변수에 선언

```java
public class lab {
    public static void main(String[] args) {
        
        final Person person = new Person("Steve"); // person 변수에 저장된 참조값 변경 불가능.
        String personName = person.getName(); // 내부에 있는 것들은 사용 가능
    }
}

class Person {
    final String name;

    public Person(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}

```

---

## 상수

1. 상수는 메서드 영역에 있는 상수풀에서 관리한다.

2. 자주 사용되거나, 명확한 고정된 값이 필요할때 주로 사용한다.

3. 대문자만 쓰는 것이 관례

---

```java
class Constant { 
    public static final double PI = 3.141592;
    public static final int KOREA_POPULATION = 51_630_000;
    public static final long EARTH_POPULATION = 7_950_000_000L;
}

public class lab {
    public static void main(String[] args) {
        System.out.println(Constant.PI);
        System.out.println(Constant.KOREA_POPULATION);
        System.out.println(Constant.EARTH_POPULATION);
        
    }
}

```
상수는 상수풀에서 관리하기 때문에, 객체를 생성하지 않고도 호출할 수 있다.

---

