## String 클래스

String 객체는 불변 객체이며, 문자열 풀을 사용해서 메모리를 효율적으로 관리하고 성능을 높인다.

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

## StringBuilder

StringBuilder는 문자열을 변경할 때, String 객체와 달리 새로운 객체를 생성하지 않고 기존 객체 내부에서 문자열을 변경하면서 사용한다. 

-> 메모리와 성능면에서 효율적이다.

---

## StringBuilder vs StringBuffer


### 공통점
- StringBuilder와 StringBuffer는 모두 가변 객체로, 문자열을 변경할 때 새로운 객체를 생성하지 않고 기존 객체 내부에서 변경한다.

- 두 클래스는 대부분의 메서드가 동일하다. // append(), insert(), delete(), reverse(), toString()

### 차이점

|특징|StringBuilder|StringBuffer|
|:---:|:---:|:---:|
동기화|X|O
사용 환경|단일 스레드|멀티 스레드
성능|빠름|느림




