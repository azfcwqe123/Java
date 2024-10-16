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

### 박싱(Boxing), 언방식(Unboxing)

```java
class lab {
    public static void main (String[] args) {

        int a = 10;
        Integer A = Integer.valueOf(a); // int -> Integer 변환, 박싱

        int b = A.intValue(); // Integer -> int 변환, 언박싱

        System.out.println("Integer A = " + A);
        System.out.println("int b = " + b);
    }
}
```
```
Integer A = 10
int b = 10
```

### 오토 박싱(Auto-Boxing), 오토 언박싱(Auto-Unboxing)

```java
class lab {
    public static void main (String[] args) {

        int a = 10;
        Integer A = a; // int -> Integer 변환, 오토 박싱

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
### 래퍼 클래스 배열

```java
class lab {
    public static void main (String[] args) {

        Integer[] arr1 = new Integer[5]; // 모든 요소가 null

        Integer[] arr2 = {1,2,3,4,5};

        for (Integer integer : arr1) {
            System.out.print(integer + " ");
        }

        System.out.println();
        
        for (Integer integer : arr2) {
            System.out.print(integer + " ");
        }
        
    }
}
```

```
null null null null null 
1 2 3 4 5 
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

        System.out.println(A==B); // 참조값 같음

        System.out.println(A.equals(B)); // 값은 같음
    }
}
```
```
true
true
```

아래는 -128 ~ 127 범위가 아닌 Integer 클래스를 생성한 예시다.
```java
class lab {
    public static void main (String[] args) {

        Integer A = 500;
        Integer B = 500;

        System.out.println(A==B); // 참조값 다름

        System.out.println(A.equals(B)); // 값은 같음
    }
}
```

```
false
true
```

캐싱되는 클래스

|Byte|-128~127|
|:---:|:---:|
Short|-128~127|
Character|0~127|
Integer|-128~127|
Long|-128~127|
Boolean|true, false|

캐싱되지 않는 클래스 -> Float, Double


---

### 래퍼 클래스의 공통 메서드들

|메서드|특징|
|:---:|:---:|
valueOf()|기본 데이터 타입을 래퍼 객체로 변환
xxxValue()|래퍼 객체를 기본 데이터 타입으로 변환
parseXxx()|문자열을 해당 기본 데이터 타입으로 변환
toString()|문자열로 변환
.compareTo()|래퍼 객체 비교, 같으면 0, 첫번째 객체가 크면 1, 작으면 -1
equlas()|래퍼 객체 비교, 같으면 true, 다르면 false
