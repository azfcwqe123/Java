## 래퍼 클래스

|기본 데이터 타입|래퍼 클래스|
|:---:|:---:|
boolean|Boolean
char|Character
byte|Byte
short|Short
int|Integer
long|Long
float|Float
double|Double

래퍼 클래스를 사용하면 기본 데이터 타입을 객체로 사용할 수 있다.

기본형 타입을 사용해야하는데, null 값이 필요할 때 사용하면 유용하다.

---

### 오토 박싱(Auto-Boxing), 오토 언박싱(Auto-Unboxing)

```java
class lab {
    public static void main (String[] args) {

        int a = 10;
        Integer A = Integer.valueOf(a); // int -> Integer 변환, 오토 박싱

        int b = A; // Integer -> int 변환, 오토 언박싱

        System.out.println("Integer A = " + A);
        System.out.println("int b = " + b);
    }
}
```
```
Integer A = 10
int b = 10
```

---

### 래퍼 클래스 비교

래퍼 클래스는 객체이기 때문에 '=='가 아닌 .equals() 메서드를 통해 비교해야한다.

성능 최적화를 위해 -128 ~ 127 범위는 Integer 클래스 안에 있는 IntegerCache라는 정적 내부 클래스에 미리 생성돼있다. 

```java
class lab {
    public static void main (String[] args) {

        Integer A = -128;
        Integer B = -128;

        System.out.println(A==B);

        System.out.println(A.equals(B));
    }
}
```
```
true
true
```

아래는 
```java
class lab {
    public static void main (String[] args) {

        Integer A = 500;
        Integer B = 500;

        System.out.println(A==B);

        System.out.println(A.equals(B));
    }
}
```

```
false
true

```
