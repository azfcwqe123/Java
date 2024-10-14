## String 클래스

String 객체는 불변 객체이며, 문자열 풀을 사용해서 메모리를 효율적으로 관리하고 성능을 높인다.

불변성 덕분에 사이드 이펙트 발생을 예방하고 멀티스레드 환경에서 안전하게 사용할 수 있다. 

```java
public class lab {
    public static void main(String[] args) {

        String str1 = "Hello"; // 문자열 풀에 생성
        String str2 = "Hello"; // 문자열 풀에 생성돼있던 참조값을 그대로 사용
        String str3 = new String("Hello"); // 문자열 풀 사용X, 힙 영역에 새로운 인스턴스를 생성


        System.out.println("------'==' 비교------");
        System.out.println(str1 == str2); // 참조값이 서로 같음
        System.out.println(str2 == str3); // 참조값이 서로 다름

        System.out.println("------equals() 비교------");

        System.out.println(str1.equals(str2)); // 같은 문자를 포함
        System.out.println(str1.equals(str3)); // 같은 문자를 포함

    }
}

```

---

### StringBuilder

StringBuilder는 문자열을 변경할 때, String 객체와 달리 새로운 객체를 생성하지 않고 기존 객체 내부에서 문자열을 변경하면서 사용한다. 

- 메모리와 성능면에서 효율적이다.

- 메서드 체이닝 기법을 사용한다.
  
---

### StringBuilder vs StringBuffer


#### 공통점
- StringBuilder와 StringBuffer는 모두 가변 객체로, 문자열을 변경할 때 새로운 객체를 생성하지 않고 기존 객체 내부에서 변경한다.

- 두 클래스는 대부분의 메서드가 동일하다. // append(), insert(), delete(), reverse(), toString()

#### 차이점

|특징|StringBuilder|StringBuffer|
|:---:|:---:|:---:|
동기화|X|O
사용 환경|단일 스레드|멀티 스레드
성능|빠름|느림

---

### String 메서드

#### length()

```java
public class lab {
    public static void main(String[] args) {

        String str = "Hello, World!";
        int n = str.length();
        System.out.println(n);
    }
}

```
```
13
```
---

#### charAt(int index)

```java
public class lab {
    public static void main(String[] args) {

        String str = "Hello, World!";
        char ch = str.charAt(4);
        System.out.println(ch);
    }
}

```

```
o
```

----

#### substring()
```java
public class lab {
    public static void main(String[] args) {

        String str = "Hello, World!";

        String a = str.substring(0,5); // [ )
        String b = str.substring(5); // [

        System.out.println(a);
        System.out.println(b);
    }
}

```

```
Hello
, World!
```

---

#### indexOf()
```java
public class lab {
    public static void main(String[] args) {

        String str = "Hello, World!";

        int index1 = str.indexOf(", World!");
        int index2 = str.indexOf("안녕하세요");

        System.out.println(index1);
        System.out.println(index2); // 찾는 값이 없을땐 -1 반환
    }
}

```

```
5
-1
```

---

#### contains()

```java
public class lab {
    public static void main(String[] args) {

        String str = "Hello, World!";

        boolean TF = str.contains("World");

        System.out.println(TF);
    }
}

```

```
true
```

---

#### compareTo()

```java
public class lab {
    public static void main(String[] args) {

        String str1 = "apple";
        String str2 = "bus";

        // 두 문자열을 사전순으로 비교. 첫번째 문자열이 두번째 문자열보다 앞에 있으면 -1, 같으면 0, 뒤에 있으면 1 반환
        int n = str1.compareTo(str2);

        System.out.println(n);
    }
}

```

```
-1
```

---

#### replace()

```java
public class lab {
    public static void main(String[] args) {

        String str = "Hello, World!";

        String a = str.replace("World", "apple");

        System.out.println(a);

    }
}

```

```
Hello, apple!
```

---

#### trim()

```java
public class lab {
    public static void main(String[] args) {

        String str = "    Hello, World!     ";

        String a = str.trim(); // 공백 제거

        System.out.println(a);
        
    }
}

```

```
Hello, World!
```

#### split()

```java
import java.util.Arrays;

public class lab {
    public static void main(String[] args) {

        String str = "AA, AO, BO, BB, OO, AB";

        String[] arr = str.split(", "); // 문자열을 주어진 정규식을 기준으로 나누고, 배열 반환

        for (String s : arr) {
            System.out.print(s + " ");
        }

    }
}

```

```
AA AO BO BB OO AB 
```

---

#### toUpperCase(), toLowerCase()

```java
import java.util.Arrays;

public class lab {
    public static void main(String[] args) {

        String str = "asASFDefdASDwd";

        System.out.println(str.toLowerCase());

        System.out.println(str.toUpperCase());
        
    }
}

```

```
asasfdefdasdwd
ASASFDEFDASDWD
```

---

#### valueOf()

```java
import java.util.Arrays;

public class lab {
    public static void main(String[] args) {

        int n = 100;
        char ch = 'F';
        boolean TF = true;

        // 기본 데이터 타입을 문자열로 반횐
        System.out.println(String.valueOf(n));
        System.out.println(String.valueOf(ch));
        System.out.println(String.valueOf(TF));
    }
}

```

```
100
F
true
```

